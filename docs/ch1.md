# 第 1 章 CSS 和 文档

层叠样式表(Cascading Style Sheets, CSS)是一种强大的工具，它可以转换文档或文档集合的表现形式，而且它几乎已经扩展到 web 的每个角落，并进入许多表面上没有 web 的环境。例如，基于 gecko 的浏览器使用 CSS 来影响浏览器 chrome 本身的表现，许多 RSS 客户端允许您将 CSS 应用于摘要和摘要条目，一些即时消息客户端使用 CSS 来格式化聊天窗口。CSS 的各个方面可以在 JavaScript 框架使用的语法中找到，甚至在 JavaScript 本身中也可以找到。到处都是 CSS！

## 1.1 (Web) 样式简史

CSS 最初是在 1994 年提出的，当时 web 刚刚开始流行。当时，浏览器为用户提供了各种样式设置功能——例如，Mosaic 中的表示首选项允许用户在每个元素的基础上定义各种字体、大小和颜色。而这些功能对文档作者却是不可用的;他们所能做的就是将一段内容标记为段落、某个级别的标题、预先格式化的文本或少数其他元素类型之一。如果一个用户配置他的浏览器，使所有一级标题(h1)的颜色为粉红色，字体为小号字体，而所有六级的标题(h6)的颜色为红色，字体为大号字体，那么，这就是他的问题了。

CSS 就是在这种环境中引入的。它的目标是提供一种简单的、声明式的样式语言，这种语言对作者来说是灵活的，最重要的是，它为作者和用户都提供了样式功能。通过“级联”的方式，这些风格可以被组合在一起并按优先级排列，这样作者和读者都有发言权——尽管读者总是拥有最后的发言权。

工作进展迅速，到 1996 年年底，CSS1 就已经完成了。当新成立的 CSS 工作组继续推进 CSS2 时，浏览器厂商们却艰难地实现了互不兼容的 CSS1。尽管每个 CSS 片段本身相当简单，但是这些片段的组合导致了一些令人惊讶的复杂行为。在早期的实现中也有一些不幸的失误，比如盒模型（box model）实现中臭名昭著的差异。这些问题威胁着 CSS 的发展，但幸运的是，一些聪明的建议被采纳，浏览器开始协调起来。在几年之内，由于不断增强的兼容性和频繁发布的新内容，例如基于 CSS 重新设计的 Wired 杂志和 [CSS 禅意花园](http://www.csszengarden.com/tr/zh-cn/)，CSS 开始逐渐流行起来。

虽然，在此之前，CSS 工作组就已在 1998 年初定稿了 CSS2 规范。CSS2 完成后，团队立即着手 CSS3 的工作，并将 CSS2 的一个明确版本称为 CSS2.1。为了顺应时代精神，CSS3 被构建为一系列(理论上)独立的模块，而不是一个的庞大的规范。这种方法也影响了当时正在开发的 XHTML 规范，出于类似的原因，该规范被划分为多个模块。

模块化 CSS3 的基本原理是，每个模块都可以按照自己的速度工作，而且特别重要的(或受欢迎的)模块可以按照 W3C 的进度前进，而不会受到其他模块的制肘。实际上，这已成为实际上的行为标准。到 2012 年初，三个 CSS3 模块(以及 CSS1 和 CSS 2.1)已经达到了完全推荐状态，即 CSS 颜色级别 3、CSS 命名空间和选择器级别 3。与此同时，有 7 个模块处于候选推荐状态，其他几十个模块处于不同的工作草案阶段。在旧的方法下，颜色、选择器和名称空间必须等到规范的其他部分完成或删除之后才能成为完整规范的一部分。由于模块化，他们不必等待。

这种方法的劣势是很难准确地指出一个具体的“CSS3 规范”。没有这种东西，也没有任何一个东西可以被这么称呼。即使其它所有的 CSS 模块在 2016 年末达到了第 3 级(虽然并没有)，已经有了第 4 级的选择器。我们会自然地将之称为 CSS4 吗？那些仍在开发中的 “CSS3” 特性要怎么称呼？例如网格布局，它甚至还没有达到级别一？

因此，我们不能指着一本大部头说“这就是 CSS3”，但我们可以通过这些功能模块的名称来谈论它们。这些灵活性模块不仅仅是弥补了它们有时造成的语义上的尴尬。(如果你想要一个近似于单一规范的东西，CSS 工作组每年都会发布“快照”文档。)

了解了这些后，我们就可以开始学习 CSS 了。不过，我们必须先深入一下标记。

## 1.2 元素（Elements)

元素是文档结构的基础。在 HTML 中，最常见的元素很容易识别，如 `p`, `table`, `span`, `a`, 和 `div`。文档中的每个元素都在其表示中起作用。

### 1.2.1 替换元素和非替换元素

虽然 CSS 依赖于元素，但并不是所有的元素的创建方式都是一样的。例如，图像和段落不是同一类型的元素，`span` and `div` 也不是。在 CSS 中，元素通常有两种生成形式:替换和非替换。

#### 替换元素

替换元素指是那些元素内容会被文档中没有直接表示的内容所替换的元素。最熟悉的 HTML 示例可能是 img 元素，它被文档本身外部的图像文件所取代。事实上，img 并没有实际的内容，你可以在这个简单的例子中看到:

```html
<img src="howdy.gif" />
```

这个标记片段只包含一个元素名和一个属性。元素不会显示任何内容，除非您将其指向某些外部内容(在本例中，是由 src 属性指定的图像)。如果您指向一个有效的图像文件，则图像将被放置在文档中。否则，它将不显示任何内容，或者浏览器将显示一个“损坏的图像”占位符。

类似地，input 元素也可以根据其类型被替换为单选按钮、复选框或文本输入框。

#### 非替换元素

大多数 HTML 元素是非替换元素。这意味着它们的内容由用户代理(通常是浏览器)在元素本身生成的框中显示。例如 `<span>hi there</span>` 是一个不可替换的元素，文本“hi there”将由用户代理显示。这适用于 HTML 中的段落、标题、表格单元格、列表和几乎所有其他内容。

### 1.2.2 元素显示角色

除了替换和非替换元素外，CSS 还采用了另两种基本类型的元素：块级元素和行内元素。还有更多的显示类型，但这俩是最基本的，也是大多数(如果未指定其它显示方式)其他显示类型所依赖的类型。对于那些已经花时间研究 HTML 标记及其在 web 浏览器中的显示的作者来说，块级方式和内联方式是很熟悉的。这些元素如图 1-1 所示。

<Figures figure="1-1">HTML 文档中的块级和行级元素</Figures>

#### 块级元素

块级元素生成一个元素框，该元素框(默认情况下)填充其父元素的内容区域，并且不能在其两侧有其他元素。换句话说，它在元素框之前和之后生成“break”。HTML 中最常见的块级元素是 p 和 div。替换元素可以是块级元素，但通常不是。

列表项是块级元素的特殊情况。除了以与其他块元素一致的方式工作外，它们还生成一个标记(通常是无序列表的项目符号和有序列表的数字)，该标记被“附加”到元素框中。除了此标记之外，列表项在其他所有方面都与其它块元素相同。

#### 行内元素（内联元素）

内联级元素在一行文本中生成一个元素框，并且不会破坏该行的流。最好的内联元素示例是 HTML 中的 a 标签。其它示例还包括 strong 和 em。这些元素不会在它们自己之前或之后生成“break”，因此它们可以出现在另一个元素的内容中，而不会中断它的显示。

请注意，虽然“块”和“内联”的名称与 HTML 中的块级和内联级元素有很多相同之处，但它们之间有一个重要的区别。在 HTML 中，块级元素不能从内联级元素派生。在 CSS 中，对于显示角色之间如何嵌套没有限制。为了了解它是如何工作的，让我们考虑一个 CSS 属性 display。

为了了解它是如何工作的，让我们考虑一个 CSS 属性 display。

你可能已经注意到了这里有许多取值，只有其中三个是我提到过的： `block`、 `inline` 和 `list-item`。这些取值的大部分会在本书其他部分介绍；例如 `grid` 和 `inline-grid` 涵盖在介绍栅格布局的独立的一章，跟表格相关的值都包含在介绍 CSS 表格布局的章节中。

现在我们把注意力放在 `block` 和 `inline` 上，看下面的代码：

```html
<body>
  <p>This is a paragraph with <em>an inline element</em> within it.</p>
</body>
```

这里有两个块级元素（`body`和`p`）和一个行内元素（`em`）。根据 HTML 规范， `em` 可以作为 `p` 的后代，但反过来则不行。通常 HTML 的层级结构允许行内元素作为块级元素的后代，而反过来却不行。

CSS 则没有这样的限制，你可以保持现有的标签结构，然后修改这两个元素的显示角色：

```css
p {
  display: inline;
}
em {
  display: block;
}
```

这使得元素在一个行内框里面生成了一个块级框，这在 CSS 中是完全合法的，不会破坏任何规范。但是，如果你想在 HTML 中使用相反的嵌套结构，那就有会问题了，像这样：

```html
<em><p>This is a paragraph improperly enclosed by an inline element.</p></em>
```

不管你如何使用 CSS 来修改它们的显示角色，这在 HTML 中都是不合法的。

修改元素的显示角色在 HTML 文档中很有用，它对 XML 文档也至关重要。XML 文档一般没有默认的显示角色，而完全依赖文档开发者去定义它们。例如，如果你想要展示下面的 XML 片段：

```html
<book>
  <maintitle>Cascading Style Sheets: The Definitive Guide</maintitle>
  <subtitle>Third Edition</subtitle>
  <author>Eric A. Meyer</author>
  <publisher>O'Reilly and Associates</publisher>
  <pubdate>November 2006</pubdate>
  <isbn type="print">978-0-596-52733-4</isbn>
</book>
<book>
  <maintitle>CSS Pocket Reference</maintitle>
  <subtitle>Third Edition</subtitle>
  <author>Eric A. Meyer</author>
  <publisher>O'Reilly and Associates</publisher>
  <pubdate>October 2007</pubdate>
  <isbn type="print">978-0-596-51505-8</isbn>
</book>
```

因为 `display` 属性的默认值是 `inline`，所以这块内容会默认被显示为行内文本，就像图 1-2 所示的那样。这样的排版不太有用。

<Figures figure="1-2">XML 文档的默认显示</Figures>

你可以用`display`来定义文档的基本板式：

```css
book,
maintitle,
subtitle,
author,
isbn {
  display: block;
}
publisher,
pubdate {
  display: inline;
}
```

这样就把 7 个元素中的 5 个设置为块级元素，2 个设置为行内元素。这意味着每个块级元素会像 HTML 中的 div 那样被处理，而 2 个行内元素会像行内元素一样被处理。

这种设置显示角色的基本能力使得 CSS 在各种场景下都非常有用。我们可以基于上面的规则，添加一些更具视觉效果的样式，然后得到如图 1-3 这样的显示效果。

<Figures figure="1-3">应用样式后的 XML 文档</Figures>

在详细学习如何编写 CSS 之前，我们先要看一下如何关联 CSS 和文档，毕竟，如果不把它们结合在一起，CSS 是无法对文档起作用的。我们从最熟悉的 HTML 设置开始。

## 1.3 连接 CSS 和 HTML

我提到过 HTML 文档存在一个固有结构，这一点值得重复一下。实际上有个旧网页开发遗留的问题：太多人忘记了文档是应该有一个内在结构的，这与视觉上的结构是完全不同的。我们急于在 Web 上创建看起来最酷的网页，我们改造转换、修饰装点，全然忽视了页面应该包含具有一些结构意义的信息。

这种结构是 HTML 和 CSS 之间关系所固有的组成部分，没有它，关系就不会存在。为了更好地理解这种结构，我们把下面这个示例的 HTML 文档拆解来看：

```html
<html>
  <head>
    <title>Eric's World of Waffles</title>
    <meta http-equiv="content-type" content="text/html; charset=utf-8" />
    <link rel="stylesheet" type="text/css" href="sheet1.css" media="all" />
    <style type="text/css">
      /* These are my styles! Yay! */
      @import url(sheet2.css);
    </style>
  </head>
  <body>
    <h1>Waffles!</h1>
    <p style="color: gray;">
      The most wonderful of all breakfast foods is the waffle—a ridged and
      cratered slab of home-cooked, fluffy goodness that makes every child's
      heart soar with joy. And they're so easy to make! Just a simple
      waffle-maker and some batter, and you're ready for a morning of aromatic
      ecstasy!
    </p>
  </body>
</html>
```

代码的应用样式后的处理结果如图 1-4 所示。

<Figures figure="1-4">简单文档</Figures>

 现在我们来看文档关联 CSS 的几种方式。

### 1.3.1 link 标签

先来看看 link 标签的用法：

```html
<link rel="stylesheet" type="text/css" href="sheet1.css" media="all" />
```

`link` 标签是一个有些被忽视的标签，但它是在 HTML 规范中存在了许多年的合法标签，一直在等着被善加利用。它最初的目的是允许 HTML 开发者把其它文档引入使用了 `link ` 标签的文档中。CSS 用它把样式表链接到文档中，如图 1-5，一个名为 `sheet1.css` 的样式表被连接到文档。

这些样式表不是 HTML 文档的一部分但仍被应用于文档中，它们被称为**外部样式表**，因为它们存在于 HTML 文档的外部（看图）。

要成功加载外部样式表， `link` 必须作为 `head` 元素的直接下级，不能放在任何其它元素中。这将使得 web 浏览器成功定位和加载样式表，并使用它包含的任何样式渲染 HTML 文档，渲染结果如图 1-5 所示。图 1-5 还展示了通过 @import 指令加载外部 `sheet2.css`。导入指令必须置于包含它们的样式表的开头，除此之外，别无限制。

<Figures figure="1-5">外部文件如何被引入文档的示例</Figures>

那么外部样式表是什么样的格式呢？和我们在前面章节中和在示例 HTML 文档中看到的那些样式一样，外部样式也是简单的规则列表，但是这些规则存储在自己的文件里面。要记住，HTML 和其它任何标记语言都不能放进样式表中——它只能包含样式规则。一个外部样式表的内容是这样的：

```css
h1 {
  color: red;
}
h2 {
  color: maroon;
  background: white;
}
h3 {
  color: white;
  background: black;
  font: medium Helvetica;
}
```

这就是它的全部内容——没有 HTML 标记或者注释，只有干净简单的样式声明。它们被存储在纯文本文件中，通常用 `.css` 作为后缀，例如 `sheet1.css`。

<Tips tips="orange">外部样式表不能包含任何文档标签，仅能出现 CSS 规则和 CSS 注释（本章后续会介绍）。外部样式表中的文档标记会导致部分或整个样式表被忽略。</Tips>

文本扩展名不是必须的，但一些比较老的浏览器仅将以 .css 作为扩展名的文件视作样式表，即便 link 标签中已指定了正确的类型 text/css。实际上，一些 web 浏览器不会将一个文件视作 text/css，除非其文件名以 .css 结尾。不过，这种行为通常可以通过修改服务器配置文件来修复。

#### 属性

对于 link 标记的其余部分，属性和值非常简单。rel 代表“关系”，在本例中，关系是 stylesheet。type 属性总是设置为 text/css。此值描述使用 link 标签加载的文档类型。这样，web 浏览器就知道 stylesheet 是一个 CSS 样式表，这将决定浏览器如何处理它导入的数据。毕竟，将来可能还会使用其它样式语言，所以声明您正在使用的 hich 语言是很重要的。

接下来介绍 href 属性。这个属性的值是样式表的 URL。这个 URL 可以是绝对的，也可以是相对的，按需选择。在我们的示例中，URL 是相对的。它也可以是类似于 http://meyerweb.com/sheet1.css 这样的东西。

最后还有有一个 media 属性。此属性的值是一个或多个媒体描述符，指明样式表的目标媒体类型和这些媒体特性的规则，每个规则由逗号分隔。因此，例如，你可以在屏幕和投影媒体中使用链接样式表:

```html
<link
  rel="stylesheet"
  type="text/css"
  href="visual-sheet.css"
  media="screen, projection"
/>
```

媒体描述符非常复杂，本章后面会详细介绍。现阶段，我们先只管用最简单的媒体类型。

注意，一篇文档可以引入超过一个样式表。

实际上，只有那些设置了 ref 属性的 link 标签引入的样式表会影响文档。所以，如果你要同时引入名为 basic.css 和 splash.css 的样式表，要像这样：

```html
<link rel="stylesheet" type="text/css" href="basic.css" />
<link rel="stylesheet" type="text/css" href="splash.css" />
```

这会使得浏览器加载这两个样式表，合并两个样式表中的规则，并将合并后的规则应用至文档。例如：

```html
<link rel="stylesheet" type="text/css" href="basic.css" />
<link rel="stylesheet" type="text/css" href="splash.css" />
<p class="a1">
  This paragraph will be gray only if styles from the stylesheet 'basic.css' are
  applied.
</p>
<p class="b1">
  This paragraph will be gray only if styles from the stylesheet 'splash.css'
  are applied.
</p>
```

这段代码中未展示的另一个关键属性是 title。这个属性不常用到，但是未来会变得很重要，而且如果使用不当，会导致不可预料的影响。为什么呢？我们会在下一章仔细讨论。

#### 备选样式表

还可以通过设置 rel 属性的值为 alternate stylesheet 定义备选样式表。备选样式表仅在用户主动选中时才会应用到文档表示层。

如果浏览器能够使用备选样式表，它将使用 link 元素的 title 属性的值来生成备选样式列表。代码如下:

```html
<link rel="stylesheet" type="text/css" href="sheet1.css" title="Default" />
<link
  rel="alternate stylesheet"
  type="text/css"
  href="bigtext.css"
  title="Big Text"
/>
<link
  rel="alternate stylesheet"
  type="text/css"
  href="zany.css"
  title="Crazy colors!"
/>
```

随后用户可以选择他们期望的样式，而浏览器也会从“默认”样式切换至用户选择的样式。图 1-6 显示了如何执行这一选择的一种方式（实际上这是 CSS 流行的早期的选择方式）。

<Figures figure="1-6">提供备选样式表选择的浏览器</Figures>

<Tips tips="blue">截止2016 年末，备选样式表已被大多数基于 Gecko 引擎的浏览器支持，例如 Firefox 和 Opera。Internet Explorer 家族的浏览器未原生支持备选样式表，但可以通过 Javascript 来支持备选样式表。而 WebKit 家族的浏览器并不支持备选样式表。对比图 1-6 中所使用的浏览器的年龄，这真的有够惊人的。</Tips>

还能通过给 title 属性赋予相同的值的方式将备选样式表分组。这就使得将站点在屏幕和打印预览时以完全不同的方式进行展示成为可能：

```html
<link
  rel="stylesheet"
  type="text/css"
  href="sheet1.css"
  title="Default"
  media="screen"
/>
<link
  rel="stylesheet"
  type="text/css"
  href="print-sheet1.css"
  title="Default"
  media="print"
/>
<link
  rel="alternate stylesheet"
  type="text/css"
  href="bigtext.css"
  title="Big Text"
  media="screen"
/>
<link
  rel="alternate stylesheet"
  type="text/css"
  href="print-bigtext.css"
  title="Big Text"
  media="print"
/>
```

若用户从用户代理的选择框中选中了 "Big Text" 备用样式表，那么 bigtext.css 将会渲染屏幕上的文档，而 print-bigtext.css 会渲染打印预览时的文档。而 sheet1.css 和 print-sheet1.css 将不会在影响任何媒体中的文档。

为什么呢？这是因为，如果你为一个拥有 ref 属性的 link 标签赋予了 titlte 属性，其就成为首选样式表。这意味着其优先级比备选样式表高，且会在文档首次显示时启用。不过，一旦你选择了备用样式表，则首选样式表将被弃用。此外，如果你指定了好几个首选样式表，启用其中一个会导致其它的都被弃用。思考以下代码示例：

```html
<link
  rel="stylesheet"
  type="text/css"
  href="sheet1.css"
  title="Default Layout"
/>
<link
  rel="stylesheet"
  type="text/css"
  href="sheet2.css"
  title="Default Text Sizes"
/>
<link
  rel="stylesheet"
  type="text/css"
  href="sheet3.css"
  title="Default Colors"
/>
```

三个 link 元素现在均被指定为首选样式表，因为它们都设置了 title 属性，但在这种情况下，仅有一个会真的生效。另外两个会被完全忽略。哪两个呢？答案是不确定，因为 HTML 并没有提供启用或忽略首选样式表的方法。

如果没有给样式表赋予一个 title，那么其就会成为永久生效的样式表，一直影响着文档的展示。通常情况下，这是用户期望的行为。

### 1.3.2 style 元素

style 元素能包裹样式，且直属于文档：

```html
<style type="text/css">
  ...;
</style>
```

style 元素应该总是使用 type 属性；对于 CSS 文档，正确的取值是 "text/css"，就像 link 元素中的一样。

如上面的例子所示，style 元素应该总是以 `<style type="text/css">` 开头，随后跟着一项或多项样式配置，并以关闭标签 `</style>` 作为结束。也可以为 style 元素指定 media 属性，功能与 link 元素中的一致。位于起始和结束 style 标签之间的样式被称为文档样式或内嵌样式（因为这种样式表是内嵌在文档中的）。它除了能包含将会影响文档的样式之外，还能包含通过 @import 指令引入的多个外部样式表。

### 1.3.3 @import 指令

现在我们要讨论 style 标签中的成员。首先是与 link 功能类似的 @import 指令：

```css
@import url(sheet2.css);
```

就像 link 一样，@import 可用于指示浏览器加载外部样式表，并使用其中的样式渲染 HTML 文档。唯一主要的区别是语法和命令的位置。如你所见，@import 位于 style 内部。它必须位于其它 CSS 规则之前，否则不会生效。思考以下示例：

```html
<style type="text/css">
  @import url(styles.css); /* @import comes first */
  h1 {
    color: gray;
  }
</style>
```

与 link 类似，文档中可以使用多个 @import 语句。而与 link 不同的是，每个 @import 指令引入的样式表总是会被加载和使用。通过 @import 无法指定备用样式表。所以，有以下代码：

```css
@import url(sheet2.css);
@import url(blueworld.css);
@import url(zany.css);
```

三个样式表均会被加载，且它们的样式规则会被用于渲染文档。

与 link 一样，你可以在样式 URL 之后添加媒体描述符，限制被导入的样式表仅针对一个或多个媒体。

```css
@import url(sheet2.css) all;
@import url(blueworld.css) screen;
@import url(zany.css) projection, print;
```

第 8 页的“link 标签”提到媒体描述符可以十分复杂，而在第 20 章的媒体依赖样式我们会详细介绍。

如果你有一个需要引用另一个外部样式表的外部样式表，@import 就变得非常有用。由于外部样式表不能包含任何 HTML 文档标记，那么就不能使用 link 元素，但可以用 @import。因此，你可能有如下的一个外部样式表：

```css
@import url(http://example.org/library/layout.css);
@import url(basic-text.css);
@import url(printer.css) print;
body {
  color: red;
}
h1 {
  color: blue;
}
```

当然，可能样式不完全一样，但好在你学会了这个方法。注意前文例子中提到的绝对和相对 Url。就像 link 一样，这里两种形式都可以用。

同时注意出现在样式表开头的 @import 指令，就像示例文档中的一样。CSS 要求 @import 指令出现在样式文件中所有具体样式的前面。出现在具体样式（如 body {color: red;}）之后的 @import 指令将会被用户代理忽略。

<Tips tips="orange">Windows 上老版本的 Internet Explorer 不会忽略任何 @import 指令，即便是那些出现在具体样式规则之后的。由于其它浏览器都会忽略未未正确放置的 @import 指令，这导致很容易将 @import 指令放在错误的位置，修改其它浏览器中的显示方式。</Tips>

### 1.3.4 HTTP Linking

还有一种鲜为人知的关联 CSS 与文档的方式：通过 HTTP 请求头。

在 Apache 下，可以通过在 .htaccess 文件中添加一个指向 CSS 文件的引用的方法完成。

```css
Header add Link "</ui/testing.css>;rel=stylesheet;type=text/css"
```

这会使得所有支持此功能的浏览器将该样式文件与所有受此 .htaccess 文件影响的文档进行关联。浏览器会像处理通过 link 引入的样式表一样处理此样式表。或者，你可以使用另一个种更高效的方法，在 httpd.conf 文件中添加一条等效的规则：

```css
<Directory /path/to/ /public/html/directory>
Header add Link "</ui/testing.css>;rel=stylesheet;type=text/css"
</Directory>
```

在支持的浏览器中，两种方法的效果一致。唯一的区别是声明 linking 的位置。

你可能注意到了术语“支持的浏览器”。截止 2017 年底，用户数较多的支持 HTTP linking 样式表的浏览器主要是 Firefox 家族和 Opera。这就限制了这项技术基本只能在开发环境下，基于这些浏览器使用。这种情况下，你可以在开发站点（不是正式站）上利用测试服上的 HTTP linking 。这也是一个有趣方法对 Webkit 和 Internet Explorer 家族隐藏样式，假定你有这么做的原因。

<Tips tips="blue">在常见的脚本语言中，如 PHP 和 IIS，也有等效的技巧，因为这些语言都支持发送 HTTP 头。还可以在服务端渲染模式下，利用这些语言显式地在文档头中写入一个 link 元素。就浏览器的支持性而言，这种方法兼容性更强：每个浏览器都支持 link 元素。</Tips>

### 1.3.5 内联样式

对于只想为特定元素配置少量样式的场景，无需使用内嵌或外部样式，可以使用 HTML 的 style 属性来设置内联样式：

```html
<p style="color: gray;">
  The most wonderful of all breakfast foods is the waffle—a ridged and cratered
  slab of home-cooked, fluffy goodness...
</p>
```

style 属性可以应用至任何 HTML 标签，除了那些在 body 之外的标签（例如 head 或 title）。

style 属性的语法相当普通。实际上，它与 style 容器中声明的非常相似，除了此处的花括号被双引号代替。所以， `<p style="color: maroon; background: yellow;">` 会将段落的文本颜色设置栗色，背景色设置未黄色。文档的其它部分不会收此声明的影响。

注意，在内联样式中，你只能放一个声明块，而不是完整的样式表。因此，你不能将 @import 语句放入 style 属性，也不能在其中包含完整的规则。你唯一可以放入 style 属性的就是花括号之间的样式。

一般不推荐使用 style 属性。实际上，除了 HTML 语言之外，其它语言，例如 XML 中不太可能出现这种用法。当你将样式放入 style 属性时，集中管理样式文件的优点，如完全控制一份文档的表现形式，或 web 服务器上所有文档的部分样式就被否定了。很多情况下，内联样式都没有比 font 标签好多少，尽管它在处理视觉效果方面更加灵活和多样化。

## 1.4 样式表内容

说了这么多，究竟啥是样式表的实际内容呢？如你所知，像这些：

```css
h1 {
  color: maroon;
}
body {
  background: yellow;
}
```
诸如此类的样式组成了内嵌样式，不论简单或复杂，短的或长的。很少有文档会不包含任何规则，虽然可以通过一些简单的 @import 指令而不显示类似上例中的规则。在读本书的后续内容之前，要了解一些最高级的规则——哪些内容能进入样式表，哪些不能。

### 1.4.1 标记

样式表中不能有标记语法。这很明显，不过你会大吃一惊。唯一的例外是 HTML 注释标记，因为历史原因，它可以出现在 style 元素之内：

```html
<style type="text/css">
  <!--
  h1 {color: maroon;}
  body {background: yellow;}
  -->
</style>
```

懂了吗，老铁。

### 1.4.2 规则结构

要更详细的介绍规则的原则，让我们把它拆成几部分。

每条规则有两个基本组成：选择器和声明块。声明块由一条或多条声明组成，且每条声明都是一个属性-值对。每个样式表由一系列规则组成。图 1-7 显示了一条规则的组成部分。

<Figures figure="1-7">规则结构</Figures>

位于规则左侧的选择器定义了文档的哪部分会受到影响。在图 1-7 中，h1 元素被选中了。若选择器为 p，则所有的 p （段落）都会被选中。

规则的右侧是声明块，由一条或多条声明组成。每条声明都由一个 CSS 属性和值组成。在图 1-7 中，该声明块包含两条声明。第一条语句使得部分文档的前景色为红色，第二条语句会使得部分文档内容的背景色为黄色。所以，该文档中所有的 h1 元素（由选择器指定）都会被格式化为红色字体，黄色背景。

### 1.4.3 供应商前缀

有时候，你会看到一些 CSS 前面有中划线和标签，例如： `-o-border-image`。这些被称作供应商前缀，是浏览器开发商将属性、值或 CSS 的其它位的标识为实验性的或宣誓所有权（有可能两者都有）。截止 2016 年底，只有几个供应商前缀，而最常见的如表 1-1 所示。

| 前缀   | 供应商                                             |
| -------- | -------------------------------------------------- |
| -epub-   | International Digital Publishing Forum ePub format |
| -moz-    | Mozilla-based 浏览器 (例如 Firefox)             |
| -ms-     | Microsoft Internet Explorer                        |
| -o-      | Opera-based 浏览器                               |
| -webkit- | Webkit-based 浏览器 (例如 safari and Chrome)    |

如表 1-1 所示，常见的供应商前缀是一个中划线，一个标签，一个中划线。虽然，有部分厂商错误的省略了开头的中划线。

供应商前缀的使用和滥用历史又长又曲折，且超出了本书的范围。可以这么说，它们起初是供应商测试新特性的一种新方法，加速提升了互操作性，无需考虑这些遗留行为是否会与其它浏览器不兼容。这避免了一系列会在早期扼杀 CSS 的问题。不幸的是，前缀属性随后被 web 开发者大量使用，结果导致了一系列新的问题。

截止 2016 年底，随着旧前缀属性慢慢从浏览器实现中移除，供应商前缀正在逐渐减少。你完全有可能不写任何前缀 CSS，但可能会在别的地方或旧项目代码中看到它。

### 1.4.4 空格处理方式

CSS 对规则间的空白符不怎么敏感，对规则内的空白符完全不感冒，虽然有一点点例外。

一般来说，CSS 处理空白符的方式与 HTML 一致：连续空白符会被压缩为单个空格后进行解析。因此，你能以以下方式格式化虚拟的彩虹规则：

```css
rainbow: infrared red orange yellow green blue indigo violet ultraviolet;
rainbow: infrared red orange yellow green blue indigo violet ultraviolet;
rainbow: infrared red orange yellow green blue indigo violet ultraviolet;
```

还可以用其它你能想到的分隔方式。唯一的限制是分隔符必须是空白符：空格、制表符(tab)、或换行符，可以独立使用，也可以组合使用， 爱用几个用几个。

类似的，你可以用空白符以任何你喜欢的风格格式化规则。下面是无穷可能中的五种：

```css
html{color:black;}
body {
  background:white;
}
p {
  color: gray;
}
h2 {
  color: 
  silver;
}
ol {
  color
  :
  silver;
}
```

从第一条规则可以看出，大量的空格会被忽略。实际上，这是在最小化的 CSS 就是这样的，它会尽可能的移除所有空白符。前两个规则之后的规则逐渐使用更多的空白符，直到最后一个规则中几乎所有可以分离到其行上的东西都被使用为止。

所有这些方法都是可用的，所有你需要选择最有意义的格式，即最容易阅读和坚持的格式。某些地方必须使用空白符。最常见的例子是值中的一系列关键字，如虚拟彩虹示例。它们必须以空白符分隔。

### 1.4.5 CSS 注释

CSS 允许注释。它非常类似 C/C++ 的注释，由 `/*` 和 `*/` 包裹：

```css
/* This is a CSS1 comment */
```

注释可以像 C++ 中的一样分布在多行：

```css
/* This is a CSS1 comment, and it
can be several lines long without
any problem whatsoever. */
```

请牢记 CSS 注释是无法嵌套的。所以，下面的例子是错误的：

```css
/* 
  This is a comment, in which we find another comment, which is WRONG
  /* Another comment */
  and back to the first comment
*/
```

<Tips tips="orange">一种不小心创建“嵌套”注释的的场景是临时将一大块本来就包含注释的样式进行注释。由于 CSS 不允许嵌套注释，“外层”注释会在遇到“内层”注释的结束标记时结束。</Tips>

不幸的是，并没有能注释“本行剩余内容”的语法，例如 // 或 #。CSS 中唯一的注释方法是 /* */。因此，如果你要在一行中放置注释，你需要特别留意其位置。例如，以下是正确的摆放方式：

```css
h1 {
  color: gray;
} /* 本条 CSS 注释包含好几行 */
h2 {
  color: silver;
} /* 内容，不过，因为其跟随在具体的样式 */
p {
  color: white;
} /* 之后，每行注释都需要被 */
pre {
  color: gray;
} /* 注释语法正确包裹。 */
```

以下例子中，若每行注释未被正确的关闭，则大部分的样式会因为成为注释的一部分而失效：

```css
h1 {
  color: gray;
} /* 本条 CSS 注释包含好几行
h2 {color: silver;} 内容, 不过，因为其未被
p {color: white;} 注释语法正确包裹，后三行的
pre {color: gray;} 样式成为了注释的一部分。*/
```

在本例中，仅第一条规则(h1 {color: gray;})会被应用至文档。剩余的规则，因为是注释的一部分，会被浏览器的渲染引擎忽略。

<Tips tips="blue">CSS 转换器处理 CSS 注释时会忽略它们，就像它们并不存在，所以，会跳过处理注释中的空白符。这意味着你可以在声明规则的右侧放置注释！</Tips>

## 1.5 媒体查询参数

通过媒体查询参数，开发者可以定义浏览器应该在何种环境下使用指定样式表。过去，这是通过在 link 元素或 style 元素的 media 属性上，或 @import 的媒体描述符上，或 @media 声明上设置媒体类型的方式处理的。媒体查询通过允许作者使用所谓的媒体描述符，根据给定媒体类型的特征选择样式表，从而使这一概念更进一步。

### 1.5.1 用法

媒体查询参数可被用在以下位置：

- link 元素的 media 属性
- style 元素的 media 属性
- @import 声明的媒体描述符部分
- @media 声明的查询参数中的媒体描述符可以是简单的媒体类型，也可以是复杂媒体类型和功能的组合

### 1.5.2 简单媒体查询参数

在学习所有媒体查询参数的可能取值之前，让我们先看一些简单的媒体块。假设我们在投影设备（如幻灯片）中需要一些不同的样式。下面是两个非常简单的样式：

```css
h1 {
  color: maroon;
}
@media projection {
  body {
    background: yellow;
  }
}
```

在该例中，所有媒体中的 h1 元素均会被涂成栗色，但 body 元素仅在投影设备中会显示黄色背景。

在一份样式表中，你可以指定任意项 @media 区块，每个区块都包含了特定的媒体描述符（本章后文详细介绍）。如果你乐意的话，可以将所有的规则封装在一个 @media 区块中，像这样：

```css
@media all {
  h1 {
    color: maroon;
  }
  body {
    background: yellow;
  }
}
```

不过，这与去掉第一行和最后一行后的表现相同，这么做的实际意义不大。

<Tips tips="blue">本节中的缩进仅是为了清晰的展示。你无需缩进 @media 区块中的规则，但如果这么做能使你的 CSS 更易于阅读的话，还是推荐你这么做的。</Tips>

### 1.5.3 媒体类型

上面例子中的 projection 和 all 所处的位置就是媒体查询参数设置的位置。这些参数依赖一个术语集合，这些术语定义了具体的媒体类型和媒体参数的描述符（如 分辨率或显示器高度），决定何种情况下应该使用 CSS 区块。

最简单的媒体查询参数形式即媒体类型，最早出现在 CSS 2 中。对于不同类型的媒体，有不同简单标签：

`all` 代表所有媒体。

`print` 有视觉的用户打印文档时或展示文档的打印预览时使用。

`screen` 在一个屏幕媒体（如桌面显示器）上展示文档时使用。所有的浏览器都运行在中等屏幕的用户代理上。

<Tips tips="blue">在本文书写时，一些浏览器还支持投影，允许像播放幻灯片一样展示文档。也有几个移动设备上的浏览器支持手持(handheld)类型，不过支持方式不尽相同。</Tips>

多项媒体类型可通过逗号列表指定。下面四个例子均能将一个样式表同时应用至屏幕和打印媒体：

```html
<link type="text/css" href="frobozz.css" media="screen, print" />
<style type="text/css" media="screen, print">
  ...;
</style>
```

```css
@import url(frobozz.css) screen, print;
@media screen, print {
  ...;
}
```

在你为这些媒体类型添加更多具体功能的描述符时，事情会更加有趣，例如那些描述了指定媒体的分辨率或颜色深度的值。

### 1.5.4 媒体描述符

那些已经在 link 元素或 @import 声明中设置过媒体类型的人对媒体查询参数的放置位置会非常熟悉。以下是两种事实上等效的，在彩色打印机上应用同一份外部样式表的方法：

```html
<link
  href="print-color.css"
  type="text/css"
  media="print and (color)"
  rel="stylesheet"
/>
```

```css
@import url(print-color.css) print and (color);
```

所有能使用媒体类型的地方均可以使用媒体查询参数。这意味着，按照上一节的示例，可以在逗号分隔的列表中使用多个查询参数：

```html
<link
  href="print-color.css"
  type="text/css"
  media="print and (color), screen and (color-depth: 8)"
  rel="stylesheet"
/>
```

```css
@import url(print-color.css) print and (color), screen and (color-depth: 8);
```
只要有一个媒体查询的结果是 "true"，那么就会应用关联的样式表。因此，给定前面的 @import，在渲染至彩色打印机或彩色屏幕时均会应用 print-color.css。若在黑白打印机上打印，两个查询条件都会是 "false"，那么 print-color.css 就不会被应用于文档。在任何屏幕介质上都是如此规则，依此类推。

每个媒体描述符由一个媒体类型和一个或多个列出的媒体特性组成，每个媒体特性描述符括在括号中。如果没有提供媒体类型，则假设为 all，这使得下面两个例子等价:

```css
@media all and (min-resolution: 96dpi) {
  ...;
}
@media (min-resolution: 96dpi) {
  ...;
}
```

一般来说，媒体特性描述符的格式类似于 CSS 中的属性-值对。有一些不同之处，最明显的是一些特性可以在没有附加值的情况下指定。因此，例如，任何基于颜色的媒体将使用(color)进行匹配，而任何使用 16 位颜色深度的媒体将使用(color: 16)进行匹配。实际上，使用没有值的描述符是对描述符的真/假测试:(颜色)表示“该媒体是彩色的吗？”

多个特征描述符可以与 and logical 关键字链接。事实上，在媒体查询中有两个逻辑关键字:

`and`

将两个或更多的媒体特性链接在一起，只有所有特性都为真，查询才为真。例如，(color) and (orientation: land scape) and (min-device-width: 800px) 意味着必须满足所有三个条件：如果媒体环境有颜色，处于横向方向，并且设备的显示宽度至少为 800 像素，则使用该样式表。

`not`

否定整个查询，如果所有条件都为真，则不应用样式表。例如，not (color) and (orientation: landscape) and (min-device-width: 800px) 表示同时如果满足这三个条件，则语句被否定。因此，如果媒体环境有颜色，是横向的，并且设备的显示宽度至少为 800 像素，那么样式表将不被使用。在其它情况下，都将使用它。

注意，not 关键字只能在媒体查询的开头使用。像  (color) and not (min-device-width: 800px) 这样的代码是不合法的。在这种情况下，查询将被忽略。还要注意的是，那些太老而不能理解媒体查询的浏览器总是会跳过一个以 not 开头的样式表。没有用于媒体查询的 OR 关键字。作为代替，分隔查询列表的逗号提供了 or 的功能，print 表示“如果媒体是屏幕或打印机则应用”。screen and (max-color: 2) or (monochrome) 是无效的，会被忽略，你应该写 screen and (max-color: 2), screen and (monochrome)。

还有一个关键字 only，它被设计成故意向后不兼容(没错，真的):

`only`

用于对那些过于老的无法理解媒体查询参数的浏览器隐藏样式表。例如，仅为那些能理解媒体查询参数的浏览器，在所有媒体应用一份样式表，你可以这么写 @import url(new.css) only all。那些能理解媒体查询参数的浏览器会忽略 only 关键字，并应用样式表。而对那些无法理解媒体查询参数的浏览器，only 关键字创建了一个 only all 的媒体类型，而这种媒体类型是无效的。因此，在这些浏览器中，该样式表会被忽略。注意，only 关键字仅能用在媒体查询参数的开头。

### 1.5.5 媒体特性描述符和值类型

至此为止，我们已经在例子中看了很多媒体特性描述符了，但没有一个完整的列表。以下是一份完整的可用描述符列表（截止 2017 年末）：

- width
- min-width
- max-width
- device-width
- min-device-width
- max-device-width
- height
- min-height
- max-height
- device-height
- min-device-height
- max-device-height
- aspect-ratio
- min-aspect-ratio
- max-aspect-ratio
- device-aspectratio
- min-device-aspectratio
- max-device-aspectratio
- color
- min-color
- max-color
- color-index
- min-color-index
- max-color-index
- monochrome
- min-monochrome
- max-monochrome
- resolution
- min-resolution
- max-resolution
- orientation
- scan
- grid

除此之外，还加了两个新的值类型：

- `<ratio>`
- `<resolution>`

这些描述符和取值的完整介绍和使用方法可在第 20 章找到。

## 1.6 特性查询参数

2015 和 2016 年间，CSS 获得了在用户代理支持某项属性-值对时应用某些 CSS 块的能力。这个能力被称为特性查询参数。

它在结构上和媒体查询参数十分类似。考虑某种情况下，你只想在 color 是个受支持的属性时对元素使用 color（本该如此）。看起来像这样：

```css
@supports (color: black) {
  body {
    color: black;
  }
  h1 {
    color: purple;
  }
  h2 {
    color: navy;
  }
}
```

也就是说，如果你能识别并响应属性-值对 color: black，使用以下样式。否则，跳过这些样式。那些不理解 @supports 的用户代理会完全忽略这块内容。

特性查询参数是逐步提高样式兼容性的完美解决方案。例如，结社你想要为已存在的浮动和内联区块布局添加一些栅格布局。你可以保留原布局方案，然后在样式表中使用如下区块：

```css
@supports (display: grid) {
  section#main {
    display: grid;
  }
  /* styles to switch off old layout positioning */
  /* grid layout styles */
}
```

这块样式会被那些能理解栅格布局的浏览器引用，覆盖旧的布局样式，并应用那些使得栅格布局生效的样式。无法理解栅格布局的老旧浏览器大概率也无法理解 @supports，所以它们会忽略整个区块，好像它从未出现过一样。

特性查询参数能被循环嵌套，还可以被嵌入媒体查询参数中，反之亦然。你可以编写基于屏幕和打印机样式的响应式布局，并将这些媒体块包裹在一个 @supports (display: flex) 块中：

```css
@supports (display: flex) {
  @media screen {
    /* screen flexbox styles go here */
  }
  @media print {
    /* print flexbox styles go here */
  }
}
```

反过来，你可以在各种响应式设计媒体查询块中添加  @supports() 块：

```css
@media screen and (max-width: 30em) {
  @supports (display: flex) {
    /* small-screen flexbox styles go here */
  }
}
@media screen and (min-width: 30em) {
  @supports (display: flex) {
    /* large-screen flexbox styles go here */
  }
}
```

如何组织这些块完全取决于你。

与媒体查询块一样，特性查询块也允许逻辑操作符。假设，我们仅想在用户代理同时支持栅格布局和 CSS 形状时应用样式。以下是可能的代码：

```css
@supports (display: grid) and (shape-outside: circle()) {
  /* grid-and-shape styles go here */
}
```

这基本上相当于写以下内容:

```css
@supports (display: grid) {
  @supports (shape-outside: circle()) {
    /* grid-and-shape styles go here */
  }
}
```

但是，除了 “and” 操作之外，还有更多可用的操作。CSS 形状(在第 10 章中详细介绍)是一个很好的例子，说明为什么“或”是有用的，因为长期以来 WebKit 只通过供应商前缀属性支持 CSS 形状。因此，如果你想使用形状，你可以使用这样的特性查询块:

```css
@supports (shape-outside: circle()) or (-webkit-shape-outside: circle()) {
  /* shape styles go here */
}
```

You’d still have to make sure to use both prefixed and unprefixed versions of the shape properties, but this would let you add support for those properties backward in the WebKit release line while supporting other browsers that also support shapes, but not via prefixed properties.

> 你仍然需要确保同时使用带前缀和不带前缀的形状属性，但是这将允许在 WebKit 发布行中向后添加对这些属性的支持，同时支持其他也支持形状的浏览器，但不是通过带前缀的属性。

All this is incredibly handy because there are situations where you might want to apply different properties than those you’re testing. So, to go back to grid layout for a second, you might want to change the margins and so forth on your layout elements when grid is in use. Here’s a simplified version of that approach:

> 所有这些都非常方便，因为在某些情况下，您可能希望应用不同于测试的属性。因此，要回到网格布局，您可能需要在使用网格时更改布局元素的页边距等。下面是这种方法的一个简化版本:

```css
div#main {
  overflow: hidden;
}
div.column {
  float: left;
  margin-right: 1em;
}
div.column:last-child {
  margin-right: 0;
}
@supports (display: grid) {
  div#main {
    display: grid;
    grid-gap: 1em 0;
    overflow: visible;
  }
  div#main div.column {
    margin: 0;
  }
}
```

也可以使用否定。例如，你可以在不支持网格布局的情况下应用以下样式:

```css
@supports not (display: grid) {
  /* grid-not-supported styles go here */
}
```

你可以将逻辑运算符组合成单个查询，但是需要使用括号来保持逻辑的正确性。假设我们希望在支持颜色，且支持网格或灵活的框布局时应用一组样式。可以这样写的:

```css
@supports (color: black) and ((display: flex) or (display: grid)) {
  /* styles go here */
}
```

请注意，在逻辑的“或”部分周围还有一组括号，用于封装栅格和 flex 测试。这些额外的括号是必要的。没有它们，整个表达式将失败，块内的样式将被跳过。换句话说，不要这样做:

```css
@supports (color: black) and (display: flex) or (display: grid) {
```

 最后，您可能想知道为什么特性查询测试同时需要属性和值。毕竟，如果你使用的是形状，你需要测试的只是外形，对吧？这是因为浏览器可以很容易地支持一个属性，而不是支持它的所有值。网格布局就是一个完美的例子。假设你可以像这样测试网格支持:

```css
@supports (display) {
  /* grid styles go here */
}
```

不过，即便是 Internet Explorer 4 也支持 display 属性。任何理解 @supports 的浏览器肯定都能理解 display，而其支持的取值可能不包括 grid。这就是为什么属性和值总是在特性查询块中测试的原因。

<Tips tips="orange">牢记这些仅是特性查询，而不是正确性查询。浏览器能理解你测试的特性，但可能错误地实现了它。所以，你并未从浏览器获得其会正确支持某项功能的承诺。所有成功的查询结果仅意味着浏览器理解了你的语言，并试着实现它。</Tips>

## 1.7 总结

使用 CSS，完全改变用户代理显示元素的方式是可能的。这可以通过 display 属性在基本级别上执行，也可以通过将样式表与文档关联的不同方式执行。用户永远不会知道这是通过外部样式表还是内嵌样式表，甚至是内联样式表来完成的。外部样式表的真正重要性在于，它允许作者将站点的所有表示信息放在一个地方，并将所有文档指向那个地方。这不仅使站点更新和维护变得轻而易举，而且还有助于节省带宽，因为所有的表示都从文档中删除了。使用 @supports()，甚至可以在原生 CSS 中进行一些基本的渐进式增强。

为了充分利用 CSS 的强大功能，开发者需要知道如何将一组样式与文档中的元素关联起来。要完全理解 CSS 是如何做到这一切的，作者需要掌握 CSS 选择文档片段进行样式化的方法，这是下一章的主题。
