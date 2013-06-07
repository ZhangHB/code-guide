# HTML 和 CSS 代码儿编写指南
灵活、靠谱儿、容易维护的 HTML 和 CSS 开发标准


----------



## 目录

* [指导原则](#golden-rule)
* [HTML](#html)
  * [语法](#html-syntax)
  * [HTML5 doctype](#html5-doctype)
  * [实用性大于语义化](#pragmatism-over-semantics)
  * [属性的先后顺序](#attribute-order)
  * [用 JS 创建的 html 结构](#javascript-generated markup)
* [CSS](#css)
  * [CSS 语法](#css-syntax)
  * [样式声明的先后顺序](#declaration-order)
  * [Formatting exceptions](#formatting-exceptions)
    * [Prefixed properties](#prefixed-properties)
    * [Rules with single declarations](#rules-with-single-declarations)
  * [可读性](#human-readable)
    * [关于注释](#comments)
    * [关于类](#classes)
    * [关于选择器](#selectors)
  * [Organization](#organization)
* [Writing copy](#copy)
  * [Sentence case](#sentence-case)



----------



## 指导原则

> 甭管多少人一块儿干活儿, 写出来的代码儿都得跟一个人儿写的似的.

This means strictly enforcing these agreed upon guidelines at all times. For additions or contributions, please [file an issue on GitHub](https://github.com/mdo/code-guide).



----------



## HTML


### HTML 语法

* 用两个空格儿当缩进
* 嵌套所有的元素
* 始终都用双引号, 别用单引号
* 自结束的元素(比如 `<img>` `<hr>` 什么的)就别跟结尾写加 `/` 了

**这么写不太理想:**

````html
<!DOCTYPE html>
<html>
<head>
<title>Page title</title>
</head>
<body>
<img src='images/company-logo.png' alt='Company' />
<h1 class='hello-world'>Hello, world!</h1>
</body>
</html>
````

**这么写更好点儿:**

````html
<!DOCTYPE html>
<html>
  <head>
    <title>Page title</title>
  </head>
  <body>
    <img src="images/company-logo.png" alt="Company">
    <h1 class="hello-world">Hello, world!</h1>
  </body>
</html>
````


### HTML5 doctype

Enforce standards mode in every browser possible with this simple doctype at the beginning of every HTML page.

````html
<!DOCTYPE html>
````


### Pragmatism over semantics

Strive to maintain HTML standards and semantics, but don't sacrifice pragmatism. Use the least amount of markup with the fewest intricacies whenever possible.


### Attribute order

HTML attributes should come in this particular order for easier reading of code.

* class
* id
* data-*
* for|type|href

Such that your markup looks like:

````html
<a class="" id="" data-modal="" href="">Example link</a>
````

### JavaScript generated markup

Writing markup in a javascript file makes the content harder to find, harder to edit, and less performant. Don't do it.



----------



## CSS

### CSS syntax

* Use soft-tabs with two spaces
* When grouping selectors, keep individual selectors to a single line
* Include one space before the opening brace of declaration blocks
* Place closing braces of declaration blocks on a new line
* Include one space after <code>:</code> in each property
* Each declaration should appear on its own line
* End all declarations with a semi-colon
* Comma-separated values should include a space after each comma
* Don't include spaces after commas in RGB or RGBa colors, and don't preface values with a leading zero
* Lowercase all hex values, e.g., <code>#fff</code> instead of <code>#FFF</code>
* Use shorthand hex values where available, e.g., <code>#fff</code> instead of <code>#ffffff</code>
* Quote attribute values in selectors, e.g., <code>input[type="text"]</code>
* Avoid specifying units for zero values, e.g., <code>margin: 0;</code> instead of <code>margin: 0px;</code>

**Incorrect example:**

````css
.selector, .selector-secondary, .selector[type=text] {
  padding:15px;
  margin:0px 0px 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0 1px 2px #CCC,inset 0 1px 0 #FFFFFF
}
````

**Correct example:**

````css
.selector,
.selector-secondary,
.selector[type="text"] {
  padding: 15px;
  margin: 0 0 15px;
  background-color: rgba(0,0,0,.5);
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}
````

Questions on the terms used here? See the [syntax section of the Cascading Style Sheets article](http://en.wikipedia.org/wiki/Cascading_Style_Sheets#Syntax) on Wikipedia.


### Declaration order

Related declarations should be grouped together, placing positioning and box-model properties closest to the top, followed by typographic and visual properties.

````css
.declaration-order {
  /* Positioning */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* Box-model */
  display: block;
  float: right;
  width: 100px;
  height: 100px;

  /* Typography */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;

  /* Visual */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  /* Misc */
  opacity: 1;
}
````

For a complete list of properties and their order, please see [Recess](http://twitter.github.com/recess).


### Formatting exceptions

In some cases, it makes sense to deviate slightly from the default [syntax](#css-syntax).

#### 带前缀的属性

When using vendor prefixed properties, indent each property such that the value lines up vertically for easy multi-line editing.
当书写那些私有属性的时候，

````css
.selector {
  -webkit-border-radius: 3px;
     -moz-border-radius: 3px;
          border-radius: 3px;
}
````

In Textmate, use **Text &rarr; Edit Each Line in Selection** (&#8963;&#8984;A). In Sublime Text 2, use **Selection &rarr; Add Previous Line** (&#8963;&#8679;&uarr;) and **Selection &rarr;  Add Next Line** (&#8963;&#8679;&darr;).

#### 单个儿样式声明的书写规则

In instances where several rules are present with only one declaration each, consider removing new line breaks for readability and faster editing.

````css
.span1 { width: 60px; }
.span2 { width: 140px; }
.span3 { width: 220px; }

.sprite {
  display: inline-block;
  width: 16px;
  height: 15px;
  background-image: url(../img/sprite.png);
}
.icon           { background-position: 0 0; }
.icon-home      { background-position: 0 -20px; }
.icon-account   { background-position: 0 -40px; }
````


### 确保良好的可读性

代码儿这东西，是由开发者编写并维护的。所以得确保你的代码儿有良好的可读性，添加描述性强的注释能让别的开发者更容易看的明白。

#### 关于注释

仅仅干巴巴的描述类名或组件名称的注释不是好注释，好的注释应该能传达给阅读者更多的信息，比如描述组件的上下文结构、说明某些样式规则的目的等等。

**不好的注释，干巴巴的就写了一个组件的名称:**

````css
/* Modal header */
.modal-header {
  ...
}
````

**更好的写法，还描述了一下儿组件的内部结构:**

````css
/* Wrapping element for .modal-title and .modal-close */
.modal-header {
  ...
}
````

#### 类名

* 始终用小写字母和连接符（就是减号儿 "-"）编写类名，别用下划线和驼峰写法
* 避免各种胡乱的缩写简写什么的
* 尽可能的让类名短小精悍言简意赅简单明了
* Use meaningful names; use structural or purposeful names over presentational
* Prefix classes based on the closest parent component's base class

**Bad example:**

````css
.t { ... }
.red { ... }
.header { ... }
````

**Good example:**

````css
.tweet { ... }
.important { ... }
.tweet-header { ... }
````

#### Selectors

* Use classes over generic element tags
* Keep them short and limit the number of elements in each selector to three
* Scope classes to the closest parent when necessary (e.g., when not using prefixed classes)

**Bad example:**

````css
span { ... }
.page-container #stream .stream-item .tweet .tweet-header .username { ... }
.avatar { ... }
````

**Good example:**

````css
.avatar { ... }
.tweet-header .username { ... }
.tweet .avatar { ... }
````

### Organization

* Organize sections of code by component
* Develop a consistent commenting hierarchy
* If using multiple CSS files, break them down by component



----------



## Copy

### Sentence case

Always write copy, including headings and code comments, in [sentence case](http://en.wikipedia.org/wiki/Letter_case#Usage). In other words, aside from titles and proper nouns, only the first word should be capitalized.



----------



### Thanks

Heavily inspired by [Idiomatic CSS](https://github.com/necolas/idiomatic-css) and the [GitHub Styleguide](http://github.com/styleguide). Made with all the love in the world by [@mdo](http://twitter.com/mdo).
