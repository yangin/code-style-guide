# CSS 编码规范

*本文档的目标是使CSS代码风格保持一致，容易被理解和被维护*。

> 虽然本文档是针对CSS设计的，但是在使用各种CSS的预编译器(如less、sass、stylus等)时，适用的部分也应尽量遵循本文档的约定。

## 目录

  1. [命名](#命名)
  1. [格式](#格式)
  1. [通用](#通用)
  1. [值与单位](#值与单位)
  1. [文字编排](#文字编排)
  1. [变换与动画](#变换与动画)
  1. [响应式](#响应式)

## 命名

[1.1]()【强制】类名为有意义的英文或英文简写, 使用小写字母，以中划线分隔

```css
/* bad */
.lb { }
.List-Box { } 
.listBox { }

/* good */
.list-box { }
```

**[⬆ 返回顶部](#目录)**

## 格式

[2.1]()【强制】使用 2 个空格作为缩进。

```css
/* bad */
.selector {
    margin: 0;
    padding: 0;
}

/* good */
.selector {
  margin: 0;
  padding: 0;
}
```

[2.2]()【强制】在规则声明的左大括号 { 前加上一个空格。

```css
/* bad */
.selector{
  margin: 0;
  padding: 0;
}

/* good */
.selector {
  margin: 0;
  padding: 0;
}
```

[2.3]()【强制】规则声明的右大括号 } 独占一行。

```css
/* bad */
.selector {
  margin: 0;
  padding: 0;}

/* good */
.selector {
  margin: 0;
  padding: 0;
}
```

[2.4]()【强制】在属性的冒号 : 后面加上一个空格，前面不加空格。

```css
/* bad */
.selector {
  border-radius:50%;
  border : 2px solid white;
}

/* good */
.selector {
  border-radius: 50%;
  border: 2px solid white;
}
```

[2.5]()【强制】规则声明之间用1个空行分隔开。

```css
/* bad */
.title {
  font-size: 2rem;
}
.selector {
  border-radius: 50%;
  border: 2px solid white;
}


.per-line {
  border-radius: 50%;
  border: 2px solid white;
}


/* good */
.title {
  font-size: 2rem;
}

.selector {
  border-radius: 50%;
  border: 2px solid white;
}

.per-line {
  border-radius: 50%;
  border: 2px solid white;
}

```

[2.6]()【推荐】在一个规则声明中应用了多个选择器时，每个选择器独占一行。

```css
/* bad */
.no, .nope, .not_good {
  border-radius:50%;
  border:2px solid white;
}

/* good */
.one,
.selector,
.per-line {
  border-radius:50%;
  border:2px solid white;
}
```

[2.7]()【强制】每个属性独占一行。

```css
/* bad */
button{
  width:100px;height:50px;color:#fff;background:#00a0e9;
}

/* good */
button{
  width:100px;
  height:50px;
  color:#fff;
  background:#00a0e9;
}
```

[2.8]()【强制】>、+、~ 选择器的两边各保留一个空格。

```css
/* bad */
main>nav {
  padding: 10px;
}

label+input {
  margin-left: 5px;
}

input:checked~button {
  background-color: #69C;
}

/* good */
main > nav {
  padding: 10px;
}

label + input {
  margin-left: 5px;
}

input:checked ~ button {
  background-color: #69C;
}
```

[2.9]()【强制】列表型属性值 书写在单行时，, 后必须跟一个空格,前面没有空格

```css
/* bad */
font-family: Arial,sans-serif;
font-family: Arial , sans-serif;

/* good */
font-family: Arial, sans-serif;
```

[2.10]()【强制】属性选择器中的值必须用双引号包围。
> 为什么? css中所有文本采用双引号。

```css
/* bad */
article[character='juliet'] {
  voice-family: "Vivien Leigh", victoria, female
}

/* good */
article[character="juliet"] {
  voice-family: "Vivien Leigh", victoria, female
}
```

[2.11]()【强制】属性定义后必须以分号结尾。

```css
/* bad */
button{
  width:100px
}

/* good */
button{
  width:100px;
}
```

**[⬆ 返回顶部](#目录)**

## 通用

[3.1]()【强制】如无必要，不得为 id、class 选择器添加类型选择器进行限定。
> 为什么？在性能和维护性上，都有一定的影响。

```css
/* bad */
dialog#error,
p.danger-message {
  font-color: #c00;
}

/* good */
#error,
.danger-message {
  font-color: #c00;
}
```

[3.2]()【推荐】 选择器的嵌套层级，位置靠后的限定条件应尽可能精确。

```css
/* bad */
.page .header .login #username input {}
.comment div * {}

/* good */
#username input {}
.comment .avatar {}
```

[3.3]()【推荐】在可以使用缩写的情况下，尽量使用属性缩写。

```css
/* bad */
.post {
  font-family: arial, sans-serif;
  font-size: 12px;
  line-height: 1.5;
}

/* good */
.post {
  font: 12px/1.5 arial, sans-serif;
}
```

[3.4]()【强制】使用 border / margin / padding 等缩写时，应注意隐含值对实际数值的影响，确实需要设置多个方向的值时才使用缩写。
> 为什么？border / margin / padding 等缩写会同时设置多个属性的值，容易覆盖不需要覆盖的设定。如某些方向需要继承其他声明的值，则应该分开设置。

```css
/* centering <article class="page"> horizontally and highlight featured ones */
article {
  margin: 5px;
  border: 1px solid #999;
}

/* bad */
.page {
  margin: 5px auto; /* introducing redundancy */
}

.featured {
  border: 1px solid #69c; /* introducing redundancy */
}

/* good */
.page {
  margin-right: auto;
  margin-left: auto;
}

.featured {
  border-color: #69c;
}
```

[3.5]()【推荐】属性书写顺序

1. 位置属性(position, top, right, z-index, display, float等)
1. 大小(width, height, padding, margin)
1. 文字系列(font, line-height, letter-spacing, color- text-align等)
1. 背景(background, border等)
1. 其他(animation, transition等)

```css
/* bad */
.sidebar {
  width: 200px;
  padding: 5px;
  border: 1px solid #ddd;
  font-size: 14px;
  line-height: 20px;
  -webkit-transition: color 1s;
  -moz-transition: color 1s;
  transition: color 1s;
  background: #f5f5f5;
  color: #333;
  position: absolute;
  top: 50px;
  left: 0;
  overflow-x: hidden;
}



.sidebar {
  /* 位置属性: positioning schemes / offsets / z-indexes / display / ...  */
  position: absolute;
  top: 50px;
  left: 0;
  overflow-x: hidden;

  /* 大小: sizes / margins / paddings / ...  */
  width: 200px;
  padding: 5px;

  /* 文字系列: font / aligns / text styles / ... */
  font-size: 14px;
  line-height: 20px;

  /* 背景: colors / shadows / gradients / borders / ... */
  background: #f5f5f5;
  border: 1px solid #ddd;
  color: #333;

  /* 其他: colors / shadows / gradients / ... */
  -webkit-transition: color 1s;
    -moz-transition: color 1s;
       transition: color 1s;
}
```

[3.5]()【强制】尽量不使用 !important 声明
> 为什么？!important 会影响优先级，不合理的使用会导致部分样式失效

```css
/* bad */
.main {
  margin-top: 120px !important;
}

/* good */
.main {
  margin-top: 120px;
}
```

[3.6]()【强制】对z-index进行分层管理, 尽量让元素自然的flow。
> 为什么？过多的z-index会让图层管理混乱。

[3.7]()【强制】css 嵌套直接子元素时，使用 直接子选择器，而非后代选择器
> 为什么？后代选择器会匹配到Dom末端，这样会浪费性能

```css
/* bad */
.content .title {
  font-size: 2rem;
}

/* good */
.content > .title {
  font-size: 2rem;
}
```

[3.8]()【推荐】避免嵌套层级过多，将嵌套深度限制在 3 级。
> 为什么？这可以避免出现过于详实的 CSS 选择器，避免大量的嵌套规则。当可读性受到影响时，将之打断。推荐避免出现多于 20 行的嵌套规则出现

```css
/* bad */
.main{
  .title{
    .name{
      color:#fff
    }
  }
}

/* good */
.main-title{
  .name{
    color:#fff
  }
}
```

[3.9]()【推荐】避免使用ID选择器及全局标签选择器防止污染全局样式

```css
/* bad */
#header{
  padding-bottom: 0px;
  margin: 0em;
}

/* good */
.header{
  padding-bottom: 0px;
  margin: 0em;
}
```

**[⬆ 返回顶部](#目录)**

## 值与单位

[4.1]()【强制】文本内容必须用双引号包围
> 为什么？文本类型的内容可能在选择器、属性值等内容中

```css
/* bad */
html[lang|=zh] q:before {
  font-family: 'Microsoft YaHei', sans-serif;
  content: '“';
}

html[lang|=zh] q:after {
  font-family: "Microsoft YaHei", sans-serif;
  content: "”";
}

/* good */
html[lang|="zh"] q:before {
  font-family: "Microsoft YaHei", sans-serif;
  content: "“";
}

html[lang|="zh"] q:after {
  font-family: "Microsoft YaHei", sans-serif;
  content: "”";
}
```

[4.2]()【强制】当数值为 0 - 1 之间的小数时，省略整数部分的 0

```css
/* bad */
panel {
  opacity: 0.8
}

/* good */
panel {
  opacity: .8
}
```

[4.3]()【强制】url() 函数中的路径不加引号

```css
/* bad */
body {
  background: url("/bg.png");
}

/* good */
body {
  background: url(/bg.png);
}
```

[4.4]()【推荐】长度为 0 时须省略单位。 (也只有长度单位可省)

```css
/* bad */
.selector {
  padding: 0px 5px;
}

/* good */
.selector {
  padding: 0 5px;
}
```

[4.5]()【强制】RGB颜色值必须使用十六进制记号形式 #rrggbb, 不允许使用 rgb()。
> 带有alpha的颜色信息可以使用 rgba()。使用 rgba() 时每个逗号后必须保留一个空格。

```css
/* bad */
.selector {
  box-shadow: 0 0 2px rgba(0,128,0,.3);
  border-color: rgb(0, 128, 0);
}

/* good */
.selector {
  box-shadow: 0 0 2px rgba(0, 128, 0, .3);
  border-color: #008000;
}
```

[4.6]()【强制】颜色值可以缩写时，必须使用缩写形式。

```css
/* bad */
.selector {
  background-color: #ffffff;
}

/* good */
.selector {
  background-color: #fff;
}
```

[4.7]()【强制】颜色值不允许使用命名色值。

```css
/* bad */
.selector {
  background-color: lightgreen;
}

/* good */
.selector {
  background-color: #90ee90;
}
```

[4.8]()【推荐】颜色值中的英文字符采用小写。

```css
/* bad */
.selector {
  background: #F5F7F9;
}

/* good */
.selector {
  background: #f5f7f9;
}
```

[4.9]()【推荐】2D位置必须同时给出水平和垂直方向的位置
> 为什么？2D 位置初始值为 0% 0%，但在只有一个方向的值时，另一个方向的值会被解析为 center。为避免理解上的困扰，应同时给出两个方向的值

```css
/* bad */
.selector {
  background-position: top; /* 50% 0% */
}

/* good */
.selector {
  background-position: center top; /* 50% 0% */
}
```

**[⬆ 返回顶部](#目录)**

## 文字编排

[5.1]()【强制】font-family 属性中的字体族名称应使用字体的英文 Family Name，其中如有空格，须放置在引号中。

```css
/* bad */
h1 {
  font-family: "微软雅黑";
}

/* good */
h1 {
  font-family: "Microsoft YaHei";
}
```

[5.2]()【推荐】font-family 按「西文字体在前、中文字体在后」、「效果佳 (质量高/更能满足需求) 的字体在前、效果一般的字体在后」的顺序编写，最后必须指定一个通用字体族( serif / sans-serif )。

```css
/* bad */
.article {
  font-family: Arial, sans-serif;
}

/* good */
h1 {
  font-family: "Helvetica Neue", Arial, "Hiragino Sans GB", "WenQuanYi Micro Hei", "Microsoft YaHei", sans-serif;
}
```

[5.3]()【强制】中文环境下最小字号为 12px
> 为什么？由于电脑系统的字体渲染机制，中文在小于12px的情况下显示效果极差，难以辨认。故浏览器也做了对应的渲染限制，在中文环境下最低只能渲染到12px。

> 可通过切换浏览器或系统语言环境来查看非中文环境下的字体渲染效果

[5.4]()【推荐】font-weight 属性必须使用数值方式描述。
> CSS 的字重分 100 – 900 共九档，但目前受字体本身质量和浏览器的限制，实际上支持 400 和 700 两档，分别等价于关键词 normal 和 bold。

```css
/* bad */
h1 {
  font-weight: bold;
}

/* good */
h1 {
  font-weight: 700;
}
```

**[⬆ 返回顶部](#目录)**

## 变换与动画

[6.1]()【强制】使用 transition 时应指定 transition-property。
> 为什么？ 避免语义不明确

```css
/* bad */
.box {
  transition: all 1s;
}

/* good */
.box {
  transition: color 1s, border-color 1s;
}

```

**[⬆ 返回顶部](#目录)**

## 响应式

[7.1]()【推荐】Media Query 不得单独编排，必须与相关的规则一起定义。

> 为什么？ 防止将来重构时，将其遗漏。

```css
/* bad */

/* header styles */
/* main styles */
/* footer styles */

@media (...) {
  /* header styles */
  /* main styles */
  /* footer styles */
}

/* good */

/* header styles */
@media (...) {
  /* header styles */
}

/* main styles */
@media (...) {
  /* main styles */
}

/* footer styles */
@media (...) {
  /* footer styles */
}
```

[7.2]()【推荐】Media Query 如果有多个逗号分隔的条件时，应将每个条件放在单独一行中。

```css
/* bad */
@media
(-webkit-min-device-pixel-ratio: 2), (min--moz-device-pixel-ratio: 2),(min-resolution: 2dppx),(min-resolution: 192dpi) {
  /* Retina-specific stuff here */
}

/* good */
@media
(-webkit-min-device-pixel-ratio: 2), /* Webkit-based browsers */
(min--moz-device-pixel-ratio: 2),  /* Older Firefox browsers (prior to Firefox 16) */
(min-resolution: 2dppx),     /* The standard way */
(min-resolution: 192dpi) {     /* dppx fallback */
  /* Retina-specific stuff here */
}
```

**[⬆ 返回顶部](#目录)**
