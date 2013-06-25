# HTML 和 CSS 代码儿编写指南
灵活、靠谱儿、容易维护的 HTML 和 CSS 开发标准


----------



## 目录

* [指导原则](#golden-rule)
* [HTML](#html)
  * [语法](#html-syntax)
  * [HTML5 的文档类型](#html5-doctype)
  * [实用性大于语义化](#pragmatism-over-semantics)
  * [属性的先后顺序](#attribute-order)
  * [用 JS 创建的 html 结构](#javascript-generated markup)
* [CSS](#css)
  * [CSS 语法](#css-syntax)
  * [样式声明的先后顺序](#declaration-order)
  * [某些特殊的书写格式](#formatting-exceptions)
    * [关于私有前缀属性](#prefixed-properties)
    * [单个儿样式声明的书写规则](#rules-with-single-declarations)
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
* 用缩进嵌套所有的元素
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


### HTML5 的文档类型(Doctype)

Html5 的文档类型声明很简短，它可以用在任何 html 文档的头部，并且可以强制任何浏览器使用标准模式渲染 html 文档。

````html
<!DOCTYPE html>
````


### 实用性大于语义化

Strive to maintain HTML standards and semantics, but don't sacrifice pragmatism. Use the least amount of markup with the fewest intricacies whenever possible.


### 属性的先后顺序

HTML attributes should come in this particular order for easier reading of code.

* class
* id
* data-*
* for|type|href

Such that your markup looks like:

````html
<a class="" id="" data-modal="" href="">Example link</a>
````

### 用 JS 创建的 html 结构

Writing markup in a javascript file makes the content harder to find, harder to edit, and less performant. Don't do it.



----------



## CSS

### CSS 语法

* 用两个空格儿当缩进
* 使用组选择器的时候，确保每个选择器在单独的一行
* 在样式声明的大括号之前， 保留一个空格儿
* 把样式声明结束部分的大括号放在单独的一行
* 在每一个属性的冒号后边也保留一个空格儿
* 每一个样式声明都应该出现在他们所在的那行里
* 在每一个样式声明后边儿都写上分号儿
* 用逗号分隔的值，每一个逗号后边也要跟一个空格儿
* 但是在 RGB 或者 RGBA 的颜色值里，逗号后边儿就别加空格儿了。另外浮点值小数点儿前边儿的 0 也可以省略掉
* 小写所有的十六进制的颜色值，比如说，用 <code>#fff</code>  替换 <code>#FFF</code>
* 尽量简写十六进制的颜色值，比如，用 <code>#fff</code> 代替 <code>#ffffff</code>
* 属性选择器的属性值都得加上引号，比如, <code>input[type="text"]</code>
* 值为 0 的时候，就别写单位了，比如, <code>margin: 0px;</code> 应该写成 <code>margin: 0;</code>

**这么写不太理想:**

````css
.selector, .selector-secondary, .selector[type=text] {
  padding:15px;
  margin:0px 0px 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0 1px 2px #CCC,inset 0 1px 0 #FFFFFF
}
````

**这么写就好多了:**

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

有不理解的术语？看看维基百科上关于 [层叠样式表的语法部分](http://en.wikipedia.org/wiki/Cascading_Style_Sheets#Syntax) 的描述。


### 样式声明的书写顺序

按照声明的用途进行分组, 把用来定位的声明, 和关于盒模型的声明放在最前边, 后边紧接着写关于文字排版的声明, 用来呈现视觉的声明放在最后边.

````css
.declaration-order {
  /* 关于定位的 */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* 关于盒模型 */
  display: block;
  float: right;
  width: 100px;
  height: 100px;

  /* 关于文字排版 */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;

  /* 视觉样式 */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  /* 杂项 */
  opacity: 1;
}
````

想了解完整的例子, please see [Recess](http://twitter.github.com/recess).


### 某些特殊的书写格式

In some cases, it makes sense to deviate slightly from the default [syntax](#css-syntax).
在某些情况下, 某些样式声明跟默认语法有些出入

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

#### 选择器

* 用类选择器(Use classes over generic element tags)
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
