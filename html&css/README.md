# HTML&CSS 编码规范

## 说明
1. 文档主要参考 [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html#Background) 整理。

## 1 通用规则

### 1.1 编码风格

#### 1.1.1 协议 Protocol

尽可能为嵌入资源使用 HTTPS 协议。

除非相应的文件不能通过 HTTPS 访问，否则图片和其它媒体文件、样式表应始终使用 HTTPS 协议。

``` <!-- 不推荐: uses the HTTP protocol -->
 <script src="http://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
 
 <!-- Recommended -->
 <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
 
 /* Not recommended: omits the protocol */
 @import '//fonts.googleapis.com/css?family=Open+Sans';
 
 /* Not recommended: uses the HTTP protocol */
 @import 'http://fonts.googleapis.com/css?family=Open+Sans';
 
 /* Recommended */
 @import 'https://fonts.googleapis.com/css?family=Open+Sans';
``` 

	
### 1.2 通用格式

#### 1.2.1 缩进 Indention

使用软tab，一次缩进2个空格。不要混用 tabs 和空格。

``` 
<ul>
  <li>Fantastic
  <li>Great
</ul>
 
.example {
  color: blue;
}
```

#### 1.2.2 大小写 Capitalization

只使用小写。

所有代码均应该小写：对于HTML元素命名、特性（attribute）和特性值（除非 `text/CDATA`）、CSS 选择器(selectors)、属性和属性值均适用。

``` 
<!-- Not recommended -->
<A HREF="/">Home</A>
 
<!-- Recommended -->
<img src="google.png" alt="Google">

/* Not recommended */
color: #E5E5E5;

/* Recommended */
color: #e5e5e5;
``` 
	
#### 1.2.3 结尾空格 Trailing Whitespace

结尾不留空格。

结尾的空格没有必要，并且会给 diff 操作带来麻烦。

``` 
<!-- Not recommended -->
<p>What?_
 
<!-- Recommended -->
<p>Yes please.
``` 

### 1.3 元规则 General Meta Rules

#### 1.3.1 编码 Encoding

使用UTF-8编码 (不要带[字节序标记](https://en.wikipedia.org/wiki/Byte_order_mark))。

确保编辑器使用 UTF-8 字符编码，不带字节序标记。

使用 `<meta charset="utf-8">` 在HTML模板中指定编码（不需要为样式表单独指定）。

（更多有关何时以及如何指定编码的讨论可以参考  [Handling character encodings in HTML and CSS](https://www.w3.org/International/tutorials/tutorial-char-enc/).)）

#### 1.3.2 注释 Comments

尽可能在需要时对代码进行说明。

使用注释对代码进行解释说明：包含什么、服务了什么目的、使用相应解决方案的原因。

（此项不强制，因为完全保持代码文档完备不现实，依据项目负责程度不同，注释代码带来的好处可能有很大差别）


#### 1.3.3 待做事项 Action Items

使用 `TODO`标记待做项。

`TODO` 关键词突出待做事项，不要使用其它如  `@@` 这样的通用格式。

使用 `TODO(contact)`的格式括号中附上联系人信息（用户名或邮件列表）。

冒号后面描述事项内容  `TODO: action item`。

``` 	
{# TODO(john.doe): revisit centering #}
<center>Test</center>
 
<!-- TODO: remove optional tags -->
<ul>
  <li>Apples</li>
  <li>Oranges</li>
</ul>
```

## 2 HTML

### 2.1 风格规则 HTML Style Rules

#### 2.1.1 文档类型 Document Type

在HTML文档顶部使用 HTML5 文档类型`<!DOCTYPE html>`。

对于所有HTML文档推荐使用HTML5 (HTML 语法)： `<!DOCTYPE html>`.

(It’s recommended to use HTML, as `text/html`. Do not use XHTML. XHTML, as [`application/xhtml+xml`](https://hixie.ch/advocacy/xhtml), lacks both browser and infrastructure support and offers less room for optimization than HTML.)

不要关闭空标签（void elements），比如用 `<br>`这样的写法，而不是 `<br />`.

#### 2.1.2 `<head>`

* 始终加 title 标签；
* 对于搜索引擎友好的页面添加 `keywords` 和 `description` 元标签`<meta>` ；
* 始终加 favicon；
* 除非必须，不要在 head 中加载 javascript文件（尽量在`<body>`底部加载）。


#### 2.1.3 HTML 合法性 HTML Validity

除非对文件体积有极高的要求等特殊原因外，应尽可能使用合法有效的 HTML。

可使用类似 [W3C HTML validator](https://validator.w3.org/nu/) 的工具做合法性检查测试。

``` 	
<!-- Not recommended -->
<title>Test</title>
<article>This is only a test.

<!-- Recommended -->
<!DOCTYPE html>
<meta charset="utf-8">
<title>Test</title>
<article>This is only a test.</article>
```

#### 2.1.4 表单 `<form>`

每个表单 input 都要包含一个 `<label>` 标签， *特别是 radio 和 checkbox 元素*.

#### 2.1.5 语义 Semantics

依据用途恰当使用HTML。

如有序列表使用 `ol` ，链接使用 `a` ，按钮使用 `button` ，文章段落使用 `p` 等等。

根据用途恰当使用标签对于可访问性、复用和代码效率很重要。

``` 	
<!-- Not recommended -->
<div onclick="goToRecommendations();">All recommendations</div>

<!-- Recommended -->
<a href="recommendations/">All recommendations</a>
```

#### 2.1.6 多媒体回退 Multimedia Fallback

为多媒体内容提供备选替代内容。

对于多媒体内容，比如图片、视频、通过 `canvas` 绘制的动画对象，确保提供替代访问信息。对图片来说，可以使用有确切含义的文本 (`alt`) ，对于视频和音频如果可用的话可以使用内容文本或标题。

提供替代内容对于可访问性（accessibility）非常重要：举例来说，对于盲人用户，没有`@alt`的话就没法获取图片相关的线索。

(For images whose `alt` attributes would introduce redundancy, and for images whose purpose is purely decorative which you cannot immediately use CSS for, use no alternative text, as in `alt=""`.)

``` 	
<!-- Not recommended -->
<img src="spreadsheet.png">
 
<!-- Recommended -->
<img src="spreadsheet.png" alt="Spreadsheet screenshot.">
```

#### 2.1.7 关注分离 Separation of Concerns

表现层和行为逻辑结构分离。

严格保持结构(markup 标记)、展现（styling）和行为（scripting）分开，并且保持三者的交互尽可能少。

即：确保文档和模板只包含用作结构化目的的 HTML；把所有展现描述逻辑移到样式表中；行为逻辑放在 scripts 中。

In addition, keep the contact area as small as possible by linking as few style sheets and scripts as possible from documents and templates.

Separating structure from presentation from behavior is important for maintenance reasons. It is always more expensive to change HTML documents and templates than it is to update style sheets and scripts.

``` 	
<!-- Not recommended -->
<!DOCTYPE html>
<title>HTML sucks</title>
<link rel="stylesheet" href="base.css" media="screen">
<link rel="stylesheet" href="grid.css" media="screen">
<link rel="stylesheet" href="print.css" media="print">
<h1 style="font-size: 1em;">HTML sucks</h1>
<p>I’ve read about this on a few sites but now I’m sure:
  <u>HTML is stupid!!1</u>
<center>I can’t believe there’s no way to control the styling of
  my website without doing everything all over again!</center>

<!-- Recommended -->
<!DOCTYPE html>
<title>My first CSS-only redesign</title>
<link rel="stylesheet" href="default.css">
<h1>My first CSS-only redesign</h1>
<p>I’ve read about this on a few sites but today I’m actually
  doing it: separating concerns and avoiding anything in the HTML of
  my website that is presentational.
<p>It’s awesome!
```

#### 2.1.8 字符实体（转义符）Entity References

不要使用字符实体。

在团队间为文件和编辑器使用相同编码（UTF-8）的前提下，使用如 `&mdash;`, `&rdquo;` 或者 `&#x263a;`这样的 entity references 是没有必要的。

这里唯一的例外是对于在HTML中有特殊含义的符号如`<` 和 `&`，以及控制或不可见字符（如 no-break 空格）。

``` 	
<!-- Not recommended -->
The currency symbol for the Euro is &ldquo;&eur;&rdquo;.

<!-- Recommended -->
The currency symbol for the Euro is “€”.
```

#### 2.1.9 可选标签 Optional Tags

省略可选标签。

为了文件优化和扫描目的，可以考虑省略可选标签。 [HTML5 标准](https://whatwg.org/specs/web-apps/current-work/multipage/syntax.html#syntax-tag-omission) 定义了可以忽略的标签。

(This approach may require a grace period to be established as a wider guideline as it’s significantly different from what web developers are typically taught. For consistency and simplicity reasons it’s best served omitting all optional tags, not just a selection.)

``` 	
<!-- Not recommended -->
<!DOCTYPE html>
<html>
  <head>
  <title>Spending money, spending bytes</title>
  </head>
  <body>
  <p>Sic.</p>
  </body>
</html>

<!-- Recommended -->
<!DOCTYPE html>
<title>Saving money, saving bytes</title>
<p>Qed.
```

#### 2.1.10 `type`特性标记 `type` Attributes

样式表和脚本标签省略 `type` 特性标记。

不要为样式表使用 `type` 特性标记（除非不使用 CSS），同理不要为scripts指定 `type` （除非不使用 JavaScript）。

Specifying `type` attributes in these contexts is not necessary as HTML5 implies [`text/css`](https://whatwg.org/specs/web-apps/current-work/multipage/semantics.html#attr-style-type) and [`text/javascript`](https://whatwg.org/specs/web-apps/current-work/multipage/scripting.html#attr-script-type) as defaults. This can be safely done even for older browsers.

``` 	
<!-- Not recommended -->
<link rel="stylesheet" href="https://www.google.com/css/maia.css"
  type="text/css">

<!-- Recommended -->
<link rel="stylesheet" href="https://www.google.com/css/maia.css">

<!-- Not recommended -->
<script src="https://www.google.com/js/gweb/analytics/autotrack.js"
  type="text/javascript"></script>

<!-- Recommended -->
<script src="https://www.google.com/js/gweb/analytics/autotrack.js"></script>
```

### 2.2 HTML格式规则 HTML Formatting Rules

#### 2.2.1 通用格式 General Formatting

对每个代码块（block）/列表（list）或表格（table）元素使用单独一行，并且缩进每个子元素。

Independent of the styling of an element (as CSS allows elements to assume a different role per `display` property), put every block, list, or table element on a new line.

Also, indent them if they are child elements of a block, list, or table element.

(If you run into issues around whitespace between list items it’s acceptable to put all `li` elements in one line. A linter is encouraged to throw a warning instead of an error.)

``` 	
<blockquote>
  <p><em>Space</em>, the final frontier.</p>
</blockquote>

<ul>
  <li>Moe
  <li>Larry
  <li>Curly
</ul>

<table>
  <thead>
  <tr>
    <th scope="col">Income
    <th scope="col">Taxes
  <tbody>
  <tr>
    <td>$ 5.00
    <td>$ 4.50
</table>
```

#### 2.2.2 引号使用 HTML Quotation Marks

对于特性标记（attributes）的值使用双引号 (`""`) 而不是单引 (`''`)号标记。

``` 	
<!-- Not recommended -->
<a class='maia-button maia-button-secondary'>Sign in</a>

<!-- Recommended -->
<a class="maia-button maia-button-secondary">Sign in</a>
```

## 3 CSS

### 3.1 风格规则 CSS Style Rules

#### 3.1.1 CSS 合法性 CSS Validity

尽可能使用合法的 CSS。

Unless dealing with CSS validator bugs or requiring proprietary syntax, use valid CSS code.

使用[W3C CSS 验证器](https://jigsaw.w3.org/css-validator/) 检测合法性。

Using valid CSS is a measurable baseline quality attribute that allows to spot CSS code that may not have any effect and can be removed, and that ensures proper CSS usage.

#### 3.1.2 ID 和 Class命名 ID and Class Naming

ID 和 Class 使用有意义或者通用的名字。

总是使用反应元素目的或通用的名字作为 ID 和 class 的名字，而不是凭第一感觉或者隐晦难解的名字。

Names that are specific and reflect the purpose of the element should be preferred as these are most understandable and the least likely to change.

Generic names are simply a fallback for elements that have no particular or no meaning different from their siblings. They are typically needed as “helpers.”

Using functional or generic names reduces the probability of unnecessary document or template changes.

``` 	
/* Not recommended: meaningless */
#yee-1901 {}

/* Not recommended: presentational */
.button-green {}
.clear {}

/* Recommended: specific */
#gallery {}
#login {}
.video {}

/* Recommended: generic */
.aux {}
.alt {}
```

#### 3.1.3 ID 和 Class名字风格 ID and Class Name Style

ID 和 class起名字尽可能短，但必须时要够长（含义表达清楚）。

尽量传递出 ID 或 class 是干什么的，同时保持尽量简短。

使用此种命名方式有助于提高代码的效率和理解性。
Using ID and class names this way contributes to acceptable levels of understandability and code efficiency.

``` 	
/* Not recommended */
#navigation {}
.atr {}

/* Recommended */
#nav {}
.author {}
```

#### 3.1.4 类型选择器 Type Selectors

避免使用类型选择器修饰 ID 和 class 

Unless necessary (for example with helper classes), do not use element names in conjunction with IDs or classes.

Avoiding unnecessary ancestor selectors is useful for [performance reasons](http://www.stevesouders.com/blog/2009/06/18/simplifying-css-selectors/).

``` 	
/* Not recommended */
ul#example {}
div.error {}

/* Recommended */
#example {}
.error {}
```

#### 3.1.5 属性缩写 Shorthand Properties

属性写的尽可能简略。

CSS offers a variety of [shorthand](https://www.w3.org/TR/CSS21/about.html#shorthand) properties (like `font`) that should be used whenever possible, even in cases where only one value is explicitly set.

Using shorthand properties is useful for code efficiency and understandability.

``` 	
/* Not recommended */
border-top-style: none;
font-family: palatino, georgia, serif;
font-size: 100%;
line-height: 1.6;
padding-bottom: 2em;
padding-left: 1em;
padding-right: 1em;
padding-top: 0;

/* Recommended */
border-top: 0;
font: 100%/1.6 palatino, georgia, serif;
padding: 0 1em 2em;
``` 

#### 3.1.6 0 和单位 0 and Units

除非有明确要求，一般省略 0 值后面的单位。

Do not use units after `0` values unless they are required.

``` 	
flex: 0px; /* This flex-basis component requires a unit. */
flex: 1 1 0px; /* Not ambiguous without the unit, but needed in IE11\. */
margin: 0;
padding: 0;
```

#### 3.1.7 开头的 0 Leading 0s

省略值开头的0。

Do not use put `0`s in front of values or lengths between -1 and 1.

``` 	
font-size: .8em;
```

#### 3.1.8 十六进制表示法 Hexadecimal Notation

尽可能使用3字符的十六进制表示法。

For color values that permit it, 3 character hexadecimal notation is shorter and more succinct.

``` 	
/* Not recommended */
color: #eebbcc;

/* Recommended */
color: #ebc;
``` 

#### 3.1.9 前缀 Prefixes

（可选）为选择器添加应用相关的前缀 

In large projects as well as for code that gets embedded in other projects or on external sites use prefixes (as namespaces) for ID and class names. Use short, unique identifiers followed by a dash.

Using namespaces helps preventing naming conflicts and can make maintenance easier, for example in search and replace operations.

``` 	
.adw-help {} /* AdWords */
#maia-note {} /* Maia */
```

#### 3.1.10 ID 和 Class 分隔符 ID and Class Name Delimiters

用横线分割 ID  和 class 名。

Do not concatenate words and abbreviations in selectors by any characters (including none at all) other than hyphens, in order to improve understanding and scannability.

``` 	
/* Not recommended: does not separate the words “demo” and “image” */
.demoimage {}

/* Not recommended: uses underscore instead of hyphen */
.error_status {}

/* Recommended */
#video-id {}
.ads-sample {}
```

#### 3.1.11 Hacks

尽量避免使用user agent检测以及Hack-先尝试不同的解决方法。

It’s tempting to address styling differences over user agent detection or special CSS filters, workarounds, and hacks. Both approaches should be considered last resort in order to achieve and maintain an efficient and manageable code base. Put another way, giving detection and hacks a free pass will hurt projects in the long run as projects tend to take the way of least resistance. That is, allowing and making it easy to use detection and hacks means using detection and hacks more frequently—and more frequently is too frequently.

### 3.2 CSS格式规则 CSS Formatting Rules

#### 3.2.1 声明顺序 Declaration Order

声明条目按字母排序。
Put declarations in alphabetical order in order to achieve consistent code in a way that is easy to remember and maintain.

Ignore vendor-specific prefixes for sorting purposes. However, multiple vendor-specific prefixes for a certain CSS property should be kept sorted (e.g. -moz prefix comes before -webkit).

``` 	
background: fuchsia;
border: 1px solid;
-moz-border-radius: 4px;
-webkit-border-radius: 4px;
border-radius: 4px;
color: black;
text-align: center;
text-indent: 2em;
```

#### 3.2.2 块内容缩进 Block Content Indentation

缩进所有的块内容。

Indent all [block content](https://www.w3.org/TR/CSS21/syndata.html#block), that is rules within rules as well as declarations, so to reflect hierarchy and improve understanding.

``` 	
@media screen, projection {
 
  html {
  background: #fff;
  color: #444;
  }

}
```

#### 3.2.3 声明中止 Declaration Stops

每个声明结尾后都要加分号。

为了一致性和扩展性在每个生命结尾都要加分号。

``` 	
/* Not recommended */
.test {
  display: block;
  height: 100px
}

/* Recommended */
.test {
  display: block;
  height: 100px;
}
```

#### 3.2.4 属性名结尾 Property Name Stops

每个属性名冒号后加一个空格。

Always use a single space between property and value (but no space between property and colon) for consistency reasons.

``` 
/* Not recommended */
h3 {
  font-weight:bold;
}

/* Recommended */
h3 {
  font-weight: bold;
}
```

#### 3.2.5 声明块分离 Declaration Block Separation

在最后一个选择器和声明块之间加一个空格。

Always use a single space between the last selector and the opening brace that begins the [declaration block](https://www.w3.org/TR/CSS21/syndata.html#rule-sets).

The opening brace should be on the same line as the last selector in a given rule.

``` 	
/* Not recommended: missing space */
#video{
  margin-top: 1em;
}

/* Not recommended: unnecessary line break */
#video
{
  margin-top: 1em;
}

/* Recommended */
#video {
  margin-top: 1em;
}
```

#### 3.2.6 选择器和声明分离 Selector and Declaration Separation

使用新的行分隔选择器和声明。

Always start a new line for each selector and declaration.

``` 	
/* Not recommended */
a:focus, a:active {
  position: relative; top: 1px;
}

/* Recommended */
h1,
h2,
h3 {
  font-weight: normal;
  line-height: 1.2;
}
```

#### 3.2.7 规则分离 Rule Separation

有多个规则时使用换行分离。

Always put a blank line (two line breaks) between rules.

``` 	
html {
  background: #fff;
}

body {
  margin: auto;
  width: 50%;
}
```

#### 3.2.8 CSS 引号标记 CSS Quotation Marks

attribute 选择器和属性值使用单引号。

Use single (`''`) rather than double (`""`) quotation marks for attribute selectors or property values. Do not use quotation marks in URI values ( `url()`).

Exception: If you do need to use the `@charset` rule, use double quotation marks— [single quotation marks are not permitted](https://www.w3.org/TR/CSS21/syndata.html#charset).

``` 	
/* Not recommended */
@import url("https://www.google.com/css/maia.css");

html {
  font-family: "open sans", arial, sans-serif;
}

/* Recommended */
@import url(https://www.google.com/css/maia.css);

html {
  font-family: 'open sans', arial, sans-serif;
}
```

### 3.3 CSS 元规则 CSS Meta Rules

#### 3.3.1 注释 Comments

优先使用行注释 (`//`) ，对区块进行分组目的时可使用用分块注释。

对于不能自说明(self-documenting)的代码写详尽的注释（比如z-index、兼容性或浏览器特定的hacks）；

If possible, group style sheet sections together by using comments. Separate sections with new lines.

``` 	
/* Header */
 
#adw-header {}

/* Footer */

#adw-footer {}

/* Gallery */

.adw-gallery {}
```


### 3.4 SASS

#### 3.4.1 语法
* 使用 `.scss` 语法，而不是原始的 `.sass` 语法；
* 按逻辑对常规 CSS和 `@include`声明进行排序。（见下方）

#### 属性声明排序 Ordering of property declarations

1. 属性声明 Property declarations

    List all standard property declarations, anything that isn't an `@include` or a nested selector.

    ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      // ...
    }
    ```

2. `@include`声明 `@include` declarations

    Grouping `@include`s at the end makes it easier to read the entire selector.

    ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);
      // ...
    }
    ```

3. 嵌套选择器 Nested selectors

    Nested selectors, _if necessary_, go last, and nothing goes after them. Add whitespace between your rule declarations and nested selectors, as well as between adjacent nested selectors. Apply the same guidelines as above to your nested selectors.

    ```scss
    .btn {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);

      .icon {
        margin-right: 10px;
      }
    }
    ```

#### 变量 Variables

Prefer dash-cased variable names (e.g. `$my-variable`) over camelCased or snake_cased variable names. It is acceptable to prefix variable names that are intended to be used only within the same file with an underscore (e.g. `$_my-variable`).

#### 混入 Mixins

Mixins should be used to DRY up your code, add clarity, or abstract complexity--in much the same way as well-named functions. Mixins that accept no arguments can be useful for this, but note that if you are not compressing your payload (e.g. gzip), this may contribute to unnecessary code duplication in the resulting styles.

#### 扩展指令 Extend directive

`@extend` should be avoided because it has unintuitive and potentially dangerous behavior, especially when used with nested selectors. Even extending top-level placeholder selectors can cause problems if the order of selectors ends up changing later (e.g. if they are in other files and the order the files are loaded shifts). Gzipping should handle most of the savings you would have gained by using `@extend`, and you can DRY up your stylesheets nicely with mixins.

#### 嵌套选择器 Nested selectors

**选择器嵌套深度不要超过3层！**

```scss
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```

When selectors become this long, you're likely writing CSS that is:

* Strongly coupled to the HTML (fragile) *—OR—*
* Overly specific (powerful) *—OR—*
* Not reusable


Again: **不要使用ID选择器！**

If you must use an ID selector in the first place (and you should really try not to), they should never be nested. If you find yourself doing this, you need to revisit your markup, or figure out why such strong specificity is needed. If you are writing well formed HTML and CSS, you should **never** need to do this.


