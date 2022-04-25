---
title: HTML-CSS-JS参考手册
top: false
cover: false
toc: true
mathjax: true
date: 2021-08-15 19:20:30
password:
summary:
tags: [web,html,css,js]
categories: web
---


# HTML

## HTML结构

~~~html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <!--移动端适配代码-->
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no">
    <title>首页</title>
  </head>
  <body>
  </body>
</html>
~~~

## 基本标签

**常用标签**

| 基本标签 | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| div      | 布局容器                                                     |
| h1-h6    | 标题标签（h1权重最高 (页面中 最重要的位置logo 新闻标题)页面中只能出现一次），h3常用 |
| p        | 段落标签                                                     |
| br       | 换行标签                                                     |
| hr       | 水平分割线标签                                               |
| b        | 文本加粗                                                     |
| strong   | 文本加粗[强调]                                               |
| i        | 文本斜体                                                     |
| em       | 文本斜体                                                     |
| s        | 文本删除线                                                   |
| del      | 文本删除线[强调]                                             |
| u        | 文本下划线                                                   |
| ins      | 文本下划线[强调]                                             |
| big      | 文本放大                                                     |
| small    | 文本缩小                                                     |
| sub      | 下标                                                         |
| sup      | 上标                                                         |
| pre      | 预格式文本[原样输出]                                         |
| textarea | 文本域                                                       |
| meta     | 单标签                                                       |



**特殊字符标签**

| 转义字符 | 说明 |
| -------- | ---- |
| &nbsp ； | 空格 |
| &lt ;    | <    |
| &gt ;    | >    |



## 块级元素和行内元素

**块级元素**

```css
div
p
h1-h6
ul+li  ol+li  dl+dt+dd
hr
```

特点：

- 独占一行
- 可设置宽高，宽度默认100%，高度由内容决定（可参考父级高度设置百分比，如 height：100%）
- 可设置内外边距
- 可容纳行内元素和块级元素



**行内元素**

```css
a   span   strong   b   em   i   sub   sup   u 
```

特点：

- 和相邻行内元素在一行上

- 不能设置宽高，高度由内容决定（可通过line-height来设置高度）

- 垂直方向的padding和margin设置无效，但水平方向的padding和margin可以设置

- 只能容纳文本或行内元素

  

**特殊：a可以包裹任意块级元素 最好外面包裹一层div布局**



**行内块级元素**

特点：

* 不单独占满一行，可以看成是能够在一行里进行左右排列的块元素

- 可设置宽高（如果元素没有设置宽高，则宽高由内容决定）
- 可设置内外边距



## 行内和块级元素转换

**1. display**

~~~css
display: block; /* 行内元素转块级元素 */

display: inline; /* 块级元素转行内元素 */

display: inline-block; /* 行内块元素 */
~~~



**2. float**

若设置行内元素为：

~~~css
float: left;
/* 或者 */
float: right;
~~~

则该行内元素转换为**块级元素**，且具有浮动特性



**3. position**

若为行内元素进行定位为：

~~~css
position: absolute;
/* 或者 */
position: fixed;
~~~

会把行内元素转换为**块级元素**





# CSS

## 盒子模型

**CSS的盒子模型有两种：**

- IE 盒子模型（content部分包含了border 和padding）
- 标准W3C盒子模型，如下图：



<img src="https://www.runoob.com/images/box-model.gif" />

**盒子模型**

```css
内容(content)    内边距(padding)    边框(border)    外边距(margin)
```

许多元素将由用户代理样式表设置外边距和内边距。可以通过将元素的 margin 和 padding 设置为零来覆盖这些浏览器样式

~~~css
* {
  margin: 0;
  padding: 0;
}
~~~

在 CSS 中，width 和 height 指的是内容区域的宽度和高度。增加内边距、边框和外边距不会影响内容区域的尺寸，但是会增加元素框的总尺寸，例如

~~~css
#box {
  width: 70px;
  margin: 10px;
  padding: 5px;
}
~~~

<img src="https://www.w3school.com.cn/i/ct_css_boxmodel_example.gif">

**盒子宽高**

1.元素空间大小

~~~css
元素空间宽度 = width+ padding + margin + border
元素空间高度 = height + padding + margin + border
~~~

2.元素实际大小

~~~css
元素实际宽度 = width+ padding + margin
元素实际高度 = height + padding + margin
~~~

> 可以分成两种情况

~~~css
box-sizing: content-box; 	盒子大小 = width + padding + border（默认值）
box-sizing: border-box;		盒子大小 =  width（就是说  padding 和 border 是包含到width里面的）
~~~



## 选择器

### CSS选择器

#### 基本选择器

| 序号 | 选择器 | 含义         | 示例                        |
| ---- | ------ | ------------ | --------------------------- |
| 1    | div、p | 元素选择器   | p { color: red }            |
| 2    | #id    | id选择器     | #info { color: red }        |
| 3    | .class | 类名选择器   | .name { color: red }        |
| 4    | *      | 通配符选择器 | * { margin: 0; padding: 0;} |



#### 多元素的组合选择器

| 序号 | 选择器            | 含义           | 示例                  |
| ---- | ----------------- | -------------- | --------------------- |
| 1    | div,p     .one, p | 多元素选择器   | div,p { color: red }  |
| 2    | div p     .one p  | 后代选择器     | .one p { color: red } |
| 3    | div>p   .one>p    | 子元素选择器   | .one p { color: red } |
| 4    | div+p   .one+p    | 相邻元素选择器 | .one+p { color: red } |

~~~css
交集选择器 (div.one,  p.red)
并集选择器 (.red, p)
~~~



#### 属性选择器

| 序号 | 选择器       | 含义                                                         | 示例 |
| ---- | ------------ | ------------------------------------------------------------ | ---- |
| 1    | E[att]       | 匹配所有具有att属性的E元素（E在此处可以省略，以下同）        |      |
| 2    | E[att=val]   | 匹配所有att属性等于"val"的E元素                              |      |
| 3    | E[att~=val]  | 匹配所有att属性具有多个空格分隔的值、其中一个值等于"val"的E元素 |      |
| 4    | E[att\|=val] | 匹配所有att属性具有多个连字号分隔（hyphen-separated）的值、其中一个值以"val"开头的E元素，主要用于lang属性，比如"en"、"en-us"、"en-gb"等等 |      |

**[attr]** 

~~~css
[title] {
	color:red;
}
~~~

匹配

~~~html
<h3 title="Hello world">Hello world</h3>
<a title="W3School" href="http://w3school.com.cn">W3School</a>
~~~



**[attr=val]**

~~~css
[title=W3School] {
	color:red;
}
~~~

匹配

~~~html 
<h3 title="W3School">W3School</h3>
<a title="W3School" href="http://w3school.com.cn">W3School</a>
~~~



**[attr~=val]**

~~~css
[title~=hello] {
	color:red;
}
~~~

匹配

~~~html
<h3 title="hello world">Hello world</h3>
<p title="student hello">Hello W3School students!</h1>
~~~



**[attr\|=val]**

~~~css
[lang|=en] {
	color:red;
}
~~~

匹配

~~~html
<p lang="en">Hello!</p>
<p lang="en-us">Hi!</p>
~~~



#### 伪类

| 序号 | 选择器        | 含义                                    |
| ---- | ------------- | --------------------------------------- |
| 1    | E:first-child | 匹配父元素的第一个子元素                |
| 2    | E:link        | 匹配所有未被点击的链接                  |
| 3    | E:visited     | 匹配所有已被点击的链接                  |
| 4    | E:active      | 匹配鼠标已经其上按下、还没有释放的E元素 |
| 5    | E:hover       | 匹配鼠标悬停其上的E元素                 |
| 6    | E:focus       | 匹配获得当前焦点的E元素                 |
| 7    | E:lang(c)     | 匹配lang属性等于c的E元素                |



#### 伪元素

| 序号 | 选择器         | 含义                      |
| ---- | -------------- | ------------------------- |
| 1    | E:first-line   | 匹配E元素的第一行         |
| 2    | E:first-letter | 匹配E元素的第一个字母     |
| 3    | E:before       | 在E元素之前插入生成的内容 |
| 4    | E:after        | 在E元素之后插入生成的内容 |



### CSS3选择器

#### CSS3同级元素通用选择器

| 序号 | 选择器 | 含义                           | 示例                    |
| ---- | ------ | ------------------------------ | ----------------------- |
| 1    | E ~ F  | 匹配任何在E元素之后的同级F元素 | p ~ .one { color: red } |



#### CSS3属性选择器

| 序号 | 选择器        | 含义                             |
| ---- | ------------- | -------------------------------- |
| 1    | E[att^="val"] | 属性att的值以"val"开头的元素     |
| 2    | E[att$="val"] | 属性att的值以"val"结尾的元素     |
| 3    | E[att*="val"] | 属性att的值包含"val"字符串的元素 |



#### CSS3中与用户界面有关的伪类

| 序号 | 选择器       | 含义                                                      |
| ---- | ------------ | --------------------------------------------------------- |
| 1    | E:enabled    | 匹配表单中激活的元素                                      |
| 2    | E:disabled   | 匹配表单中禁用的元素                                      |
| 3    | E:checked    | 匹配表单中被选中的radio（单选框）或checkbox（复选框）元素 |
| 4    | E::selection | 匹配用户当前选中的元素                                    |



#### CSS 3中的结构性伪类

| 序号 | 选择器                | 含义                                                         |
| ---- | --------------------- | ------------------------------------------------------------ |
| 1    | E:root                | 匹配文档的根元素，对于HTML文档，就是HTML元素                 |
| 2    | E:nth-child(n)        | 匹配其父元素的第n个子元素，第一个编号为1                     |
| 3    | E:nth-last-child(n)   | 匹配其父元素的倒数第n个子元素，第一个编号为1                 |
| 4    | E:nth-of-type(n)      | 与:nth-child()作用类似，但是仅匹配使用同种标签的元素         |
| 5    | E:nth-last-of-type(n) | 与:nth-last-child() 作用类似，但是仅匹配使用同种标签的元素   |
| 6    | E:last-child          | 匹配父元素的最后一个子元素，等同于:nth-last-child(1)         |
| 7    | E:first-of-type       | 匹配父元素下使用同种标签的第一个子元素，等同于:nth-of-type(1) |
| 8    | E:last-of-type        | 匹配父元素下使用同种标签的最后一个子元素，等同于:nth-last-of-type(1) |
| 9    | E:only-child          | 匹配父元素下仅有的一个子元素，等同于:first-child:last-child或 :nth-child(1):nth-last-child(1) |
| 10   | E:only-of-type        | 匹配父元素下使用同种标签的唯一一个子元素，等同于:first-of-type:last-of-type或 :nth-of-type(1):nth-last-of-type(1) |
| 11   | E:empty               | 匹配一个不包含任何子元素的元素，注意，文本节点也被看作子元素 |



**p:nth-child(n)**

 选择作为其父的第二个子元素的每个 <p> 元素

```html
<style> 
p:nth-child(2) { background-color: red; }
</style>
<body>
	<h1>这是标题</h1>
	<p>第一个段落（背景红色***）</p>
	<p>第二个段落</p>
	<p>第三个段落</p>
	<p>第四个段落</p>
</body>
```



**p:first-child**

选择作为其父的首个子元素的每个 <p> 元素

```html
<style>
p:first-child { background-color: red; }
</style>
<body>
	<p>这个段落是其父元素（body）的首个子元素（背景红色***）</p>
	<h1>欢迎访问我的主页</h1>
	<p>这个段落不是其父元素的首个子元素</p>
	<div>
		<p>这个段落是其父元素（div）的首个子元素（背景红色***）</p>
		<p>这个段落不是其父元素的首个子元素</p>
	</div>
<p>你好</p>
</body>
```



**p:nth-of-type(2)**

选择作为其父的第二个 <p> 元素的每个 <p> 元素

```html
<style> 
p:nth-of-type(2) { background-color: red; }
</style>

<body>
	<h1>这是标题</h1>
	<h3>这是标题</h3>
	<p>第一个段落</p>
	<p>第二个段落（背景红色***）</p>
	<p>第三个段落</p>
	<p>第四个段落</p>
	<p>第五个段落</p>
</body>
```



**p:first-of-type**

选择作为其父的首个 <p> 元素的每个 <p> 元素

```html
<style> 
p:first-of-type { background-color: red; }
</style>

<body>
	<h1>这是标题</h1>
	<p>这是第一个段落（背景红色***）</p>
	<p>这是第二个段落</p>
	<p>这是第三个段落</p>
	<p>这是第四个段落</p>
</body>
```



**p:only-of-type**

选择作为其父的唯一 <p> 元素的每个 <p> 元素

```html
<style> 
p:only-of-type { background-color: red; }
</style>

<body>
	<div>
		<p>这是一个段落（背景红色***）</p>
	</div>
	<div>
		<p>这是一个段落</p>
		<p>这是一个段落</p>
	</div>
</body>
```



**p:only-child**

选择作为其父的唯一子元素的 <p> 元素

```html
<style> 
p:only-child { background-color: red; }
</style>

<body>
	<div>
		<p>这是一个段落（背景红色***）</p>
	</div>
	<div>
    	<p>这是一个段落</p>
		<span>这是一个 span</span>
		<p>这是一个段落</p>
	</div>
</body>
```



#### CSS3的反选伪类

| 序号 | 选择器   | 含义                           | 示例                   |
| ---- | -------- | ------------------------------ | ---------------------- |
| 1    | E:not(s) | 匹配不符合当前选择器的任何元素 | :not(p) { color: red } |



#### CSS3中的 :target 伪类

| 序号 | 选择器   | 示例                           |
| ---- | -------- | ------------------------------ |
| 1    | E:target | 匹配文档中特定"id"点击后的效果 |

```css
:target {
	color: red;
	font-size: 30px;
}
```



**E::before和E::after**

在E元素内部的开始位置和结束位创建一个元素，该元素为行内元素，且必须要结合content属性使用。

```css
div::before {
  content:"开始";
}
div::after {
  content:"结束";
}
```



E:after、E:before 在旧版本里是伪元素，CSS3的规范里“:”用来表示伪类，“::”用来表示伪元素，但是在高版本浏览器下E:after、E:before会被自动识别为E::after、E::before，这样做的目的是用来做兼容处理。

":" 与 "::" 区别在于区分伪类和伪元素

之所以被称为伪元素，是因为他们不是真正的页面元素，html没有对应的元素，但是其所有用法和表现行为与真正的页面元素一样，可以对其使用诸如页面元素一样的css样式，表面上看上去貌似是页面的某些元素来展现，实际上是css样式展现的行为，因此被称为伪元素。是伪元素在html代码机构中的展现，可以看出无法伪元素的结构无法审查



伪元素:before和:after添加的内容默认是inline元素**；这个两个伪元素的`content`属性，表示伪元素的内容,设置:before和:after时必须设置其`content`属性，否则伪元素就不起作用。



## CSS优先级

~~~css
优先级为:
!important  >  id  >  class  >  元素标签（element）
!important 比内联优先级高
~~~



## CSS继承性

**可继承样式属性**

属性存在默认继承的行为，一定是那些不会影响到页面布局的属性

~~~css
字体相关：font-size、font-weight、font-style、font-family 等
文本相关：color、line-height、white-space、text-shadow、text-align、text-indent、text-decoration、letter-spacing、word-spacing 等
其他属性：visibility、cursor 等
~~~



**不可继承样式属性**

~~~css
border、padding、margin、width、height
~~~



## CSS单位

**绝对单位**

| 单位 | 描述                       |
| :--- | :------------------------- |
| px   | 像素 (1px = 1/96th of 1in) |

**相对单位**

| 单位 | 描述                                                         |
| :--- | :----------------------------------------------------------- |
| em   | 它是描述相对于应用在当前元素的字体尺寸，所以它也是相对长度单位。一般浏览器字体大小默认为16px，则2em == 32px； |
| ex   | 依赖于英文字母小 x 的高度                                    |
| ch   | 数字 0 的宽度                                                |
| rem  | 根元素（html）的 font-size                                   |
| vw   | viewpoint width，视窗宽度，1vw=视窗宽度的1%                  |
| vh   | viewpoint height，视窗高度，1vh=视窗高度的1%                 |
| vmin | vw和vh中较小的那个。                                         |
| vmax | vw和vh中较大的那个。                                         |
| %    | 相对于父元素的长度、宽度百分比                               |

## CSS定位

CSS的定位机制共3种： **`文档流`**(标准流)、**`浮动`**和**`定位`**



~~~css
文档流：根据便签样式，自左往右，自上而下显示

浮动：一般设置浮动时，将先设置父盒子来控制可浮动范围，设置浮动后，将转化为行内块元素，脱标

定位：常用定位方式：子绝父相
	static：主要用来清除定位
	relative：相对定位，占位置，不脱标
	abosolute：绝对定位，不占位置，脱标
	fixed: 固定定位，相对于浏览器窗口进行定位

注意： 浮动和绝对定位都会脱离文档流
~~~

| position | 描述                                             |
| -------- | ------------------------------------------------ |
| static   | 自动定位（默认定位方式）                         |
| relative | 相对定位，相对于其原文档流的位置进行定位         |
| absolute | 绝对定位，相对于其上一个已经定位的父元素进行定位 |
| fixed    | 固定定位，相对于浏览器窗口进行定位               |

| 定位模式         | 是否脱标占有位置     | 是否可以使用边偏移 | 移动位置基准                     |
| ---------------- | -------------------- | ------------------ | -------------------------------- |
| 静态static       | 不脱标，正常模式     | 不可以             | 正常模式                         |
| 相对定位relative | 脱标，占有位置       | 可以               | 相对自身位置移动（自恋型）       |
| 绝对定位absolute | 完全脱标，不占有位置 | 可以               | 相对于定位父级移动位置（拼爹型） |
| 固定定位fixed    | 完全脱标，不占有位置 | 可以               | 相对于浏览器移动位置（认死理型） |



### 浮动

~~~css
浮动脱离标准流，不占位置，脱标，浮动只有左右浮动

文档流（标准流）中不占位置 display、block、 inline不遵循

float: left; 浮动
	none：默认值。元素不浮动，并会显示在其在文本中出现的位置
	left：元素向左浮动
	right：元素向右浮动
	inherit：规定应该从父元素继承 float 属性的值
~~~

<img src="https://www.w3school.com.cn/i/ct_css_positioning_floating_right_example.gif" >

<img src="https://www.w3school.com.cn/i/ct_css_positioning_floating_left_example.gif" >

如果包含框太窄，无法容纳水平排列的三个浮动元素，那么其它浮动块向下移动，直到有足够的空间。如果浮动元素的高度不同，那么当它们向下移动时可能被其它浮动元素“卡住”

<img src="https://www.w3school.com.cn/i/ct_css_positioning_floating_left_example_2.gif" >



<img src="https://s2.ax1x.com/2020/02/03/10w68P.jpg" alt="10w68P.jpg" border="0" />

### 清除浮动

清除浮动的本质：`清除浮动主要为了解决父级元素因为子级浮动引起内部高度为0 的问题`



<img src="https://s2.ax1x.com/2020/02/03/10wvVJ.jpg" alt="10wvVJ.jpg" border="0" />

<img src="https://s2.ax1x.com/2020/02/03/100FKO.jpg" alt="100FKO.jpg" border="0" />



~~~css
clear: both; 左侧和右侧均不允许出现浮动元素
	none：默认值。允许浮动元素出现在两侧
	left：在左侧不允许浮动元素
	right：在右侧不允许浮动元素
	both：在左右两侧均不允许浮动元素
	inherit：规定应该从父元素继承 clear 属性的值
~~~



**1、额外标签法**

```css
在浮动元素末尾添加<div style=“clear:both”></div>
```

说明：W3C推荐使用方式，但代码冗余性高，不推荐使用



**2、父级元素添加overflow属性**

```css
给父级添加 overflow:hidden / auto / scroll
```

触发BFC，但无法显示溢出元素



**3、使用after伪元素**

```css
.clearfix:after{
	content:"";
	display:block;
	height:0;
	clear:both; /*额外标签法*/   
	visibility:hidden; /* 隐藏盒子 */
}
.clearfix{
	*zoom:1; /*兼容IE6，IE7，IE6清楚浮动的方式 */
}
```

因为这个伪元素属于行内元素，没有宽高，所以要block转换为块级元素

```css
使用：父元素添加类：class="clearfix"
```



**4、双伪元素法，推荐使用**

```css
.clearfix:before, .clearfix:after{
	content:"";
	display:table:
}
.clearfix:after{
	clear:both;
}
.clearfix{
 *zoom:1;
} 
```

```css
使用：父元素添加类：class="clearfix"
```



### 相对定位

**`设置为相对定位的元素框会偏移某个距离。元素仍然保持其未定位前的形状，它原本所占的空间仍保留`**

~~~css
.box2 {
  position: relative;
  left: 30px;
  top: 20px;
}
~~~

<img src="https://www.w3school.com.cn/i/ct_css_positioning_relative_example.gif" >

注意，在使用相对定位时，无论是否进行移动，元素仍然占据原来的空间。因此，移动元素会导致它覆盖其它框



### 绝对定位

**`设置为绝对定位的元素框从文档流完全删除，并相对于其包含块定位，包含块可能是文档中的另一个元素或者是初始包含块。元素原先在正常文档流中所占的空间会关闭，就好像该元素原来不存在一样。元素定位后生成一个块级框，而不论原来它在正常流中生成何种类型的框`**

~~~css
.box2 {
  position: absolute;
  left: 30px;
  top: 20px;
}
~~~

<img src="https://www.w3school.com.cn/i/ct_css_positioning_absolute_example.gif" >

绝对定位的元素的位置相对于最近的`已定位祖先元素`，如果元素没有已定位的祖先元素，那么它的位置相对于`最初的包含块`

## 外边距合并

简单地说，外边距合并指的是，当两个垂直外边距相遇时，它们将形成一个外边距。合并后的外边距的高度等于两个发生合并的外边距的高度中的较大者

<img src="https://s2.ax1x.com/2020/02/03/1002J1.jpg" alt="1002J1.jpg" border="0" />

**相邻块元素垂直外边距的合并**

当上下相邻的两个`块元素`相遇时，如果上面的元素有下外边距margin-bottom，下面的元素有上外边距margin-top，则他们之间的垂直间距不是margin-bottom与margin-top之和，而是两者中的较大者。这种现象被称为相邻块元素垂直外边距的合并（也称外边距塌陷）

<img src="https://www.w3school.com.cn/i/ct_css_margin_collapsing_example_1.gif" />

**嵌套块元素垂直外边距的合并**

对于两个嵌套关系的块元素，如果父元素没有上内边距及边框，则父元素的上外边距会与子元素的上外边距发生合并，合并后的外边距为两者中的较大者，即使父元素的上外边距为0，也会发生合并。

<img src="https://www.w3school.com.cn/i/ct_css_margin_collapsing_example_2.gif" />

**其他情况**

假设有一个空元素，它有外边距，但是没有边框或填充。在这种情况下，上外边距与下外边距就碰到了一起，它们会发生合并

<img src="https://www.w3school.com.cn/i/ct_css_margin_collapsing_example_3.gif">

 如果这个外边距遇到另一个元素的外边距，它还会发生合并 

<img src="https://www.w3school.com.cn/i/ct_css_margin_collapsing_example_4.gif" >

**解决方案**

* 可以为父元素定义1像素的上边框或上内边距
* 可以为父元素添加`overflow:hidden`

~~~css
兄弟和兄弟之间	垂直方向相遇 
1.浮动 定位特性 
2.给父级 overflow:hidden; 溢出的处理  hidden隐藏  bfc
3.给父级 display:inline-block;
~~~



## BFC(块级格式化上下文)

> BFC块级格式化上下文，是一个独立的布局环境，其中的元素布局是不受外界的影响

**它决定了块级元素如何对它的内容进行布局，以及与其他元素的关系和相互关系**

​	块级元素：父级（块元素）

​	内容：子元素（块元素）

​	其他元素：与内容同级别的兄弟元素

**相互作用：BFC里的元素与外面的元素不会发生影响 **



**什么情况下可以触发BFC**

~~~css
1. float属性不为none
2. position为absolute或fixed
3. display为inline-block, table-cell, table-caption, flex, inline-flex
4. overflow不为visible( hidden、scroll、auto)
~~~



**BFC布局规则特性**

* 在BFC中，内部的盒子会在垂直方向，一个接一个地排列

* 在BFC中，盒子垂直方向的距离由margin决定，属于同一个BFC的两个相邻盒子的margin会发生重叠

* 在BFC中，每一个盒子（块盒与行盒）的左外边缘（margin-left）会触碰到容器的左边缘(border-left)，对于从左往右的格式化，否则相反，即使存在浮动也是如此

* BFC的区域不会与浮动盒子产生交集，而是紧贴浮动盒子边缘
* BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此

* 计算BFC的高度时，自然也会检测浮动或者定位的盒子高度



**BFC的主要作用**

* 利用BFC避免垂直margin重叠
* 清除元素内部浮动
* 自适应右侧盒子布局





**`利用BFC避免垂直margin重叠`**

~~~html
<style>
    p {
        color: #f55;
        background: #fcc;
        width: 200px;
        line-height: 100px;
        text-align: center;
        margin: 100px;
    }
</style>
<body>
    <p>Haha</p>
    <p>Hehe</p>
</body>
~~~

<img src="http://p5.qhimg.com/t01b47b8b7d153c07cc.png" >

两个p盒子的实际垂直距离为100px，而不是200px，其实就是外边距合并问题

根据BFC规则：在BFC中，盒子垂直方向的距离由margin决定，属于同一个BFC的两个相邻盒子的margin会发生重叠

**解决办法：**我们可以让把第二个p用div包起来，然后激活它使其成为一个BFC

~~~html
<style>
    p {
        color: #f55;
        background: #fcc;
        width: 200px;
        line-height: 100px;
        text-align: center;
        margin: 100px;
    }
    .wrap {
        overflow: hidden;
    }
</style>
<body>
    <p>Haha</p>
    <div class="wrap">
        <p>Hehe</p>
    </div>  
</body>
~~~



**`清除元素内部浮动`**

~~~html
<style>
.parent {
    border: 5px solid #fcc;
    width: 300px;
 }
 
.child {
    border: 5px solid #f66;
    width: 100px;
    height: 100px;
    float: left;
}
</style>
<body>
    <div class="parent">
        <div class="child"></div>
        <div class="child"></div>
    </div>
</body>
~~~

<img src="http://p1.qhimg.com/t016035b58195e7909a.png" >

由于子盒子设置了float浮动，脱离了文档流，导致父盒子高度为0

根据BFC规则：计算BFC的高度时，自然也会检测浮动或者定位的盒子高度

**解决办法：**只要把父元素设为BFC就可以清理子元素的浮动了，最常见的用法就是在父元素上设置`overflow: hidden`样式，对于IE6加上zoom:1就可以了

~~~css
.parent {
    overflow: hidden;
}
~~~

<img src="http://p2.qhimg.com/t016bbbe5236ef1ffd5.png" />



**`自适应右侧盒子布局`**

~~~html
<style>
    .box {
        width: 300px;
        position: relative;
    }

    .left {
        width: 100px;
        height: 150px;
        float: left;
        background: #f66;
    }

    .right {
        height: 200px;
        background: #fcc;
    }
</style>

<body>
    <div class="box">
        <div class="left"></div>
        <div class="right"></div>
    </div>
</body>
~~~

<img src="http://p1.qhimg.com/d/inn/4055c62a/4dca44a927d4c1ffc30e3ae5f53a0b79.png" >



BFC规则：

​	在BFC中，每一个盒子（块盒与行盒）的左外边缘（margin-left）会触碰到容器的左边缘(border-left)，对于从左往右的格式化，否则相反，即使存在浮动也是如此

​	BFC的区域不会与浮动盒子产生交集，而是紧贴浮动盒子边缘

**解决办法：**通过触发right生成BFC， 来实现自适应两栏布局

~~~css
.right {
    overflow: hidden;
}
~~~

当触发main生成BFC后，这个新的BFC不会与浮动的left重叠。因此会根据包含块的宽度，和left的宽度，自动变窄。效果如下

<img src="http://p6.qhimg.com/t01077886a9706cb26b.png" >



**BFC布局与普通文档流布局区别**                  
普通文档流布局规则

~~~
1. 浮动的元素是不会被父级计算高度
2. 非浮动元素会覆盖浮动元素的位置
3. margin会传递给父级
4. 两个相邻元素上下margin会重叠
~~~

BFC布局规则

~~~
1. 浮动的元素会被父级计算高度（父级触发了BFC）
2. 非浮动元素不会覆盖浮动元素位置（非浮动元素触发了BFC）
3. margin不会传递给父级（父级触发了BFC）
4. 两个相邻元素上下margin不会重叠（给其中一个元素增加一个父级，然后让他的父级触发BFC）           
~~~

## IFC(行级格式化上下文)

IFC布局规则

~~~
1. 内联元素会在水平方向一个个地放置
2. IFC地高度是由最高盒子的高度决定地
3. 当一行不够放置的时候会自动切换到下一行
4. 内部元素水平方向的margin、padding、border有效，垂直方向上无效
~~~



## CSS3-flex布局

### flex 简介

也叫**`伸缩布局`**

> ​	布局的传统解决方案，基于盒状模型，依赖 display 属性 + position属性 + float属性。它对于那些特殊布局非常不方便，比如，垂直居中就不容易实现。
>
> ​	CSS3在布局方面做了非常大的改进，使得我们对块级元素的布局排列变得十分灵活，适应性非常强，其强大的伸缩性，在响应式开中可以发挥极大的作用。

​	2009年，W3C 提出了一种新的方案----Flex 布局，可以简便、完整、响应式地实现各种页面布局。目前，它已经得到了所有浏览器的支持，这意味着，现在就能很安全地使用这项功能

<img src="http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071003.jpg" />



Flex 是 Flexible Box 的缩写，意为**`弹性布局`**，用来为盒状模型提供最大的灵活性。

**任何一个容器都可以指定为 Flex 布局**

~~~css
.box{
  display: flex;
}
~~~

**行内元素也可以使用 Flex 布局**

~~~css
.box{
  display: inline-flex;
}
~~~

**Webkit 内核的浏览器，必须加上-webkit前缀**

~~~css
.box{
  display: -webkit-flex; /* Safari */
  display: flex;
}
~~~

注意，设为 Flex 布局以后，子元素的`float`、`clear`和`vertical-align`属性将失效



### 基本概念

采用 Flex 布局的元素，称为 Flex 容器（flex container），简称**容器**。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称**项目**

<img src="http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071004.png" />

容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end；交叉轴的开始位置叫做cross start，结束位置叫做cross end。

项目默认沿主轴排列。单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size。



主轴：默认是水平方向

侧轴：默认是垂直方向



### 容器属性

#### 一个简单的例子

~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>flex布局</title>
    <style>
        * {
            padding: 0;
            margin: 0;
        }
        .box {
            width: 500px;
            height: 200px;
            background-color: #ccc;
            color: #666;
            margin: 0 auto;
            /* 设置父容器的为伸缩盒子 */
            display: flex;
            /* 设置子元素在主轴方向上的排列方式 */
            /* justify-content: flex-start; */
        }
        .left {
            flex: 1; /* flex是用来设置当前伸缩子项占据剩余空间的比例值 */
            height: 200px;
            background-color: pink;
        }
        .right {
            flex: 4;
            height: 200px;
            background-color: skyblue;
        }
    </style>
</head>
<body>
	<div class="box">
    	<div class="left">flex: 1=100</div>
    	<div class="right">flex: 4=400</div>
	</div>
</body>
</html>
~~~

<img src="https://s2.ax1x.com/2020/02/03/10cyXq.png" alt="10cyXq.png" border="0" />

#### flex-direction

`flex-direction`属性决定主轴的方向

~~~css
.box {
  flex-direction: row | row-reverse | column | column-reverse;
}

row（默认值）：主轴为水平方向，起点在左端。
row-reverse：主轴为水平方向，起点在右端。
column：主轴为垂直方向，起点在上沿。
column-reverse：主轴为垂直方向，起点在下沿。
~~~

<img src="http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071005.png" />



 #### flex-wrap

默认情况下，flex容器的子元素会强制一行显示，造成原来的子元素宽度变化

~~~css
.box{
  flex-wrap: nowrap | wrap | wrap-reverse;
}

nowrap（默认）：不换行，强制一行内显示
wrap：自动换行显示，第一行在上方
wrap-reverse:自动换行且反向
~~~

（1）nowrap（默认）：强制一行内显示

<img src="http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071007.png" />

（2）wrap：自动换行显示

<img src="http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071008.jpg" />

（3）wrap-reverse:自动换行且反向

<img src="http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071009.jpg" />



#### flex-flow

`flex-flow`属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap

~~~css
.box {
  flex-flow: <flex-direction> || <flex-wrap>;
}
~~~

<img src="https://s2.ax1x.com/2020/02/03/10gdDx.png" alt="10gdDx.png" border="0" />

<img src="https://s2.ax1x.com/2020/02/03/10gBVK.png" alt="10gBVK.png" border="0" />

<img src="https://s2.ax1x.com/2020/02/03/10gDUO.png" alt="10gDUO.png" border="0" />





#### justify-content

`justify-content`属性定义了项目在主轴上的对齐方式

~~~css
.box {
  justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;
}

flex-start（默认值）：左对齐
flex-end：右对齐
center： 居中
space-between：两端对齐，项目之间的间隔都相等。
space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
space-evenly: 间隔相等
~~~

<img src="https://s2.ax1x.com/2020/02/03/10gmgs.png" alt="10gmgs.png" border="0" />

<img src="http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071010.png" />



#### align-items

`align-items`属性定义项目在交叉轴上如何对齐

~~~css
.box {
  align-items: flex-start | flex-end | center | baseline | stretch;
}

flex-start：交叉轴的起点对齐。
flex-end：交叉轴的终点对齐。
center：交叉轴的中点对齐。
baseline: 项目的第一行文字的基线对齐。
stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
~~~

<img src="https://s2.ax1x.com/2020/02/03/10g3UU.png" alt="10g3UU.png" border="0" />

<img src="http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071011.png" />

#### align-content

`align-content`属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

~~~css
.box {
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}

flex-start：与交叉轴的起点对齐。
flex-end：与交叉轴的终点对齐。
center：与交叉轴的中点对齐。
space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
stretch（默认值）：轴线占满整个交叉轴。
~~~

<img src="http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071012.png" />



### 项目属性

#### flex-grow

`flex-grow`属性定义项目的放大比例，默认为 0，即如果存在剩余空间，也不放大

~~~css
.item {
  flex-grow: <number>; /* default 0 */
}
~~~

<img src="https://s2.ax1x.com/2020/02/03/10gWrt.png" alt="10gWrt.png" border="0" />

<img src="http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071014.png" />

如果所有项目的`flex-grow`属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的`flex-grow`属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍



#### flex-shrink

`flex-shrink`属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小

~~~css
.item {
  flex-shrink: <number>; /* default 1 */
}
~~~



<img src="https://s2.ax1x.com/2020/02/03/10g7GQ.png" alt="10g7GQ.png" border="0" />

<img src="http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071015.jpg" />

如果所有项目的`flex-shrink`属性都为1，当空间不足时，都将等比例缩小。如果一个项目的`flex-shrink`属性为0，其他项目都为1，则空间不足时，前者不缩小。

负值对该属性无效



#### flex basis

`flex-basis`属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为`auto`，即项目的本来大小

~~~css
.item {
  flex-basis: <length> | auto; /* default auto */
}
~~~

可以设为跟`width`或`height`属性一样的值（比如350px），则项目将占据固定空间



#### flex属性

`flex`属性是`flex-grow`, `flex-shrink` 和 `flex-basis`的简写，默认值为`0 1 auto`。后两个属性可选。

~~~css
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
~~~

该属性有两个快捷值：`auto` (`1 1 auto`) 和 none (`0 0 auto`)。

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。



#### align-self

`align-self`属性允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。默认值为`auto`，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`。

~~~css
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
~~~

<img src="http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071016.png" />

该属性可能取6个值，除了auto，其他都与align-items属性完全一致。

## CSS 注意点

### line-height: 0 的情况

想要画下图这个轮播图按钮来着，一个<div>，中间三个<span>搞定

设置<span>为inline-block，然后设置宽高，margin-top和margin-bottom一样的话，<span>就会在<div>里垂直居中了对吧，然而并没有。<div>的高度总是比算出来的高了那么点，使得<span>并没有很完美垂直居中，怪怪的。

~~~vue
<template>
  <div>
    <div class="father">
      <span></span>
      <span></span>
      <span></span>
    </div>
  </div>
</template>

<style lang="less">
.father {
  width: 100px;
  margin: 50px auto;
  line-height: 30px;
  background-color: pink;
  span {
    display: inline-block;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    background-color: blue;
  }
}
</style>
~~~

结果

<img src="https://i.niupic.com/images/2020/02/04/6mSo.png"/>

如图并没有垂直居中，也不是margin和padding导致

如果在span里加入文本（123或者其他）或者空格符：&nbsp , 不影响显示

~~~vue
<template>
  <div>
    <div class="father">
      <span>1</span>
      <span>1</span>
      <span>1</span>
    </div>
  </div>
</template>
~~~

<img src="https://i.niupic.com/images/2020/02/04/6mSp.png" />

在不要文本和空格符的情况下，可以给父元素加上：line-height: 0 解决此问题

~~~vue
<template>
  <div>
    <div class="father">
      <span></span>
      <span></span>
      <span></span>
    </div>
  </div>
</template>

<style lang="less">
.father {
  width: 100px;
  margin: 50px auto;
  line-height: 30px;
  background-color: pink;
  line-height: 0;
  span {
    display: inline-block;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    background-color: blue;
  }
}
</style>
~~~

结果

<img src="https://i.niupic.com/images/2020/02/04/6mSq.png" />

给父元素添加： padding: 10px 20px;

<img src="https://i.niupic.com/images/2020/02/04/6mSr.png" />

### font-size: 0 的情况

看一个例子

~~~vue
<template>
  <div>
    <div class="box">
      <div>1</div>
      <div>2</div>
      <div>3</div>
    </div>
  </div>
</template>

<style lang="less">
.box {
  width: 90px;
  height: 60px;
  margin: 50px auto;
  border: 1px solid #ccc;
  div {
    display: inline-block;
    width: 30px;
    font-size: 14px;
    box-sizing: border-box;
    border: 1px solid green;
  }
}
</style>
~~~

按道理说，3个div应该在一行显示，但是效果并没有在一行显示

<img src="https://i.niupic.com/images/2020/02/04/6mSs.png" />

这就是上文说到的原因，我们在box下添加font-size:0;再看看效果

~~~vue
<style lang="less">
.box {
  width: 90px;
  height: 60px;
  margin: 50px auto;
  border: 1px solid #ccc;
  font-size: 0;
  div {
    display: inline-block;
    width: 30px;
    font-size: 14px;
    box-sizing: border-box;
    border: 1px solid green;
  }
}
</style>
~~~

结果

<img src="https://i.niupic.com/images/2020/02/04/6mSt.png" />

可以看到这才是我们想要的结果，因此在实际开发中，为了更好的还原设计稿，在父元素很有必要设置font-size:0，避免莫名其妙的间距。





## CSS技巧

### 长文本处理

默认：字符太长溢出了容器

<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/40ade871ebd34a53a87b5fdac31190b8~tplv-k3u1fbpfcp-zoom-1.image" />

字符超出部分换行

<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7c5d1b30df0041258c0ae35a496d5e78~tplv-k3u1fbpfcp-zoom-1.image" />

字符超出位置使用连字符

<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9f85b1c16a5c4dbfa549650794659553~tplv-k3u1fbpfcp-zoom-1.image" />

### 文本超出省略

#### 单行文本超出省略

~~~css
.line-1 {
    overflow: hidden; /* 溢出隐藏 */
	text-overflow: ellipsis; /* 超出部分显示 省略号 */
	white-space: nowrap; /* 强制一行内显示 */
}
~~~

<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cb0075e0ceed4533b35b44db7e6a2b08~tplv-k3u1fbpfcp-zoom-1.image" />



#### 多行文本超出省略

~~~css
.line-2 {
    overflow: hidden;
	text-overflow: ellipsis;
	display: -webkit-box;
	-webkit-line-clamp: 2;
	-webkit-box-orient: vertical;
}
~~~



<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/88afb6a8f2824d4487267f6ff7f3e49c~tplv-k3u1fbpfcp-zoom-1.image" />



### 水平垂直居中

#### 单行的文本、行内元素、行内块元素

**水平居中**

此类元素需要水平居中，则父级元素必须是块级元素，且父级元素上需要这样设置样式

~~~css
.parent {
    text-align: center;
}
~~~

**垂直居中**

方法一：通过设置上下内间距一致达到垂直居中的效果

~~~css
.single-line {
    padding-top: 10px;
    padding-bottom: 10px;
}
~~~

方法二：通过设置 height 和 line-height 一致达到垂直居中

~~~css
.single-line {
    height: 100px;
    line-height: 100px;
}
~~~



**5.CSS实现垂直水平居中（块级元素）---------------------------------------------------------------------------------------------**

实现css垂直水平的方式有很多，下面就写出几种常用的方法



2.父元素相对定位，子元素绝对对位+`margin`负值



> 未知宽度

1. 定位+

   ```
   transform
   ```


5.`flex`布局+`margin`

```html
<style>
    .father {
        width: 500px;
        height: 300px;
        background: lightcoral;
        display: flex;
     }
     .son {
        background: lightblue;
    margin: auto;
      }
</style>
<div class="father">
    <div class="son">我要垂直水平居中</div>
</div>
```

> 效果 ![QQ截图20190626195024.png](https://img.cdn.lsyblog.com/QQ%E6%88%AA%E5%9B%BE20190626195024.png)

1



#### 固定宽高的块级盒子

**水平居中**

给div设置一个宽度，然后添加`margin: 0 auto`属性

```css
.box {
	width: 100px;
    height: 100px;
    background: red;
    margin: 0 auto;
}
```



**水平垂直居中**

~~~html
<style>
    .box {
        width: 500px;
        height: 400px;
        background-color: pink;
        position: relative;
    }

    .son {
        width: 200px;
        height: 100px;
        background-color: blue;
        position: absolute;
        top: 50%;
        left: 50%;
        margin-top: -50px;
        margin-left: -100px;
    }
</style>

<body>
    <div class="box">
        <div class="son"></div>
    </div>
</body>
~~~

~~~html
<style>
    .box {
        width: 500px;
        height: 400px;
        background-color: pink;
        position: relative;
    }

    .son {
        width: 200px;
        height: 100px;
        background-color: blue;
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        margin: auto;
    }
</style>

<body>
    <div class="box">
        <div class="son"></div>
    </div>
</body>
~~~





#### 不固定宽高的块级盒子

**方法一：absolute + transform （常用）**

~~~css
<style>
    .box {
        width: 500px;
        height: 400px;
        background-color: pink;
        position: relative;
    }

    .son {
        width: 200px;
        height: 100px;
        background-color: blue;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }
</style>

<body>
    <div class="box">
        <div class="son"></div>
    </div>
</body>
~~~



**方法二：flex （常用）**

~~~html
<style>
    .box {
        width: 500px;
        height: 400px;
        background-color: pink;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .son {
        width: 200px;
        height: 100px;
        background-color: blue;
    }
</style>

<body>
    <div class="box">
        <div class="son"></div>
    </div>
</body>
~~~



**方法三：flex + margin**

~~~html
<style>
    .box {
        width: 500px;
        height: 400px;
        background-color: pink;
        display: flex;
    }

    .son {
        width: 200px;
        height: 100px;
        background-color: blue;
        margin: auto;
    }
</style>

<body>
    <div class="box">
        <div class="son"></div>
    </div>
</body>
~~~





**方法4：line-height + vertical-align**

<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2cca3c98ae284d1aa6db063739df6e2a~tplv-k3u1fbpfcp-zoom-1.image" />



**方法5：writing-mode**

<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a345ddcd7bad462eb390b4688cb29c31~tplv-k3u1fbpfcp-zoom-1.image" />



**方法6：table-cell**

<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/317b0670c9fe4c90bb8b77f3f90d8c79~tplv-k3u1fbpfcp-zoom-1.image" />



**方法7：grid**

<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1b509172aabc4a3580c3eb57953755f5~tplv-k3u1fbpfcp-zoom-1.image" />



<img src="https://s2.ax1x.com/2020/02/03/10BZOU.jpg" alt="10BZOU.jpg" border="0" />

**让块级元素里的多行文字垂直居中**

> 这里抛出这样一个问题，如下，让块里的多行文字垂直居中？一说到垂直居中就会想到，单行文字垂直居中line-height等于height；块级元素垂直居中，position定位或者flex布局。但这里我介绍display：table和table-cell是如何让多行文字垂直居中的

**display：table-cell** 加上 **vertical-align：middle** 使高度不同的元素都垂直居中，其中div的display：inline-block使几个div在同一行显示。

~~~html
<div class="parent">
    <p class="son">
        会议认为，党的十八大以来，我国经济发展取得历史性成就、
        发生历史性变革，为其他领域改革发展提供了重要物质条件。经济实力
        再上新台阶，经济年均增长7.1%，成为世界经济增长的主要动力源和稳定器。
    </p>
</
~~~

~~~css
.parent {
    display: table;
    width: 300px;
    height: 300px;
    text-align: center;
}
.son {
    display: table-cell;
    vertical-align: middle;
    height: 200px;
    background-color: yellow;
}
~~~



### 移动端1像素解决方案

在移动端web开发中，UI设计稿中设置边框为1像素，前端在开发过程中如果出现border:1px，测试会发现在retina屏机型中，1px会比较粗，即是较经典的移动端1px像素问题

**伪类+transform**

原理：把原先元素的border去掉，然后利用:before或者:after重做border，并transform的scale缩小一半，原先的元素相对定位，新做的border绝对定位

~~~css
/*手机端实现真正的一像素边框*/
.border-1px, .border-bottom-1px, .border-top-1px, .border-left-1px, .border-right-1px {
    position: relative;
}

/*线条颜色 黑色*/
.border-1px::after, .border-bottom-1px::after, .border-top-1px::after, .border-left-1px::after, .border-right-1px::after {
    background-color: #000;
}

/*底边边框一像素*/
.border-bottom-1px::after {
    content: "";
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 1px;
    transform-origin: 0 0;
}

/*上边边框一像素*/
.border-top-1px::after {
    content: "";
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 1px;
    transform-origin: 0 0;
}

/*左边边框一像素*/
.border-left-1px::after {
    content: "";
    position: absolute;
    left: 0;
    top: 0;
    width: 1px;
    height: 100%;
    transform-origin: 0 0;
}

/*右边边框1像素*/
.border-right-1px::after {
    content: "";
    box-sizing: border-box;
    position: absolute;
    right: 0;
    top: 0;
    width: 1px;
    height: 100%;
    transform-origin: 0 0;
}

/*边框一像素*/
.border-1px::after {
    content: "";
    box-sizing: border-box;
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    border: 1px solid gray;
}


/*设备像素比*/
/*显示屏最小dpr为2*/
@media (-webkit-min-device-pixel-ratio: 2) {
    .border-bottom-1px::after, .border-top-1px::after {
        transform: scaleY(0.5);
    }

    .border-left-1px::after, .border-right-1px::after {
        transform: scaleX(0.5);
    }

    .border-1px::after {
        width: 200%;
        height: 200%;
        transform: scale(0.5);
        transform-origin: 0 0;
    }
}

/*设备像素比*/
@media (-webkit-min-device-pixel-ratio: 3)  {
    .border-bottom-1px::after, .border-top-1px::after {
        transform: scaleY(0.333);
    }

    .border-left-1px::after, .border-right-1px::after {
        transform: scaleX(0.333);
    }

    .border-1px::after {
        width: 300%;
        height: 300%;
        transform: scale(0.333);
        transform-origin: 0 0;
    }
}
/*需要注意<input type="button">是没有:before, :after伪元素的*/
~~~





**去除图片底侧空白缝隙**

有个很重要特性你要记住： 图片或者表单等行内块元素，他的底线会和父级盒子的基线对齐。这样会造成一个问题，就是图片底侧会有一个空白缝隙。

解决的方法就是：  

1. 给img vertical-align:middle | top等等。  让图片不要和基线对齐。

​	  2.   给img 添加 display：block; 转换为块级元素就不会存在问题了。

~~~css
vertical-align:baseline;
	1.图片下方间隙问题
		解决方法 => 给img任意值覆盖baseline
	2.图文的对齐方式  行内元素或者行内块元素之间的对齐方式
		解决方法  顶部对齐  给两个元素同时加上vertical-align:top;	
top 对齐元素(你设置了vertical的元素)的顶端 与line-box 的顶端对齐
bottom  对齐元素(你设置了vertical的元素)的底端 与line-box 的底端对齐
middle (常用)对齐元素 的中线 父元素的基线加上小写x
~~~



**解决inline-block元素设置overflow:hidden属性导致相邻行内元素向下偏移**

```css
.wrap {
  display: inline-block;
  overflow: hidden
	vertical-align: bottom
}
```

**超出部分显示省略号**

```css
// 单行文本
.wrap {
	overflow:hidden;/*超出部分隐藏*/
	text-overflow:ellipsis;/*超出部分显示省略号*/
	white-space:nowrap;/*规定段落中的文本不进行换行 */
}
// 多行文本
.wrap {
    width: 100%;
    overflow: hidden;
    display: -webkit-box;   //将对象作为弹性伸缩盒子模型显示  *必须结合的属性*
    -webkit-box-orient: vertical;   //设置伸缩盒对象的子元素的排列方式  *必须结合的属性*
    -webkit-line-clamp: 3;   //用来限制在一个块元素中显示的文本的行数
    word-break: break-all;   //让浏览器实现在任意位置的换行 *break-all为允许在单词内换行*
}
```

**css实现不换行、自动换行、强制换行**

```css
//不换行
.wrap {
  white-space:nowrap;
}
//自动换行
.wrap {
  word-wrap: break-word;
  word-break: normal;
}
//强制换行
.wrap {
  word-break:break-all;
}
```

**CSS实现文本两端对齐**

```css
.wrap {
    text-align: justify;
    text-justify: distribute-all-lines;  //ie6-8
    text-align-last: justify;  //一个块或行的最后一行对齐方式
    -moz-text-align-last: justify;
    -webkit-text-align-last: justify;
}
```

**实现文字竖向排版**

```css
// 单列展示时
.wrap {
    width: 25px;
    line-height: 18px;
    height: auto;
    font-size: 12px;
    padding: 8px 5px;
    word-wrap: break-word;/*英文的时候需要加上这句，自动换行*/  
}
// 多列展示时
.wrap {
    height: 210px;
    line-height: 30px;
    text-align: justify;
    writing-mode: vertical-lr;  //从左向右    
    writing-mode: tb-lr;        //IE从左向右
    //writing-mode: vertical-rl;  -- 从右向左
    //writing-mode: tb-rl;        -- 从右向左
}
```

**使元素鼠标事件失效**

```css
.wrap {
    // 如果按tab能选中该元素，如button，然后按回车还是能执行对应的事件，如click。
	pointer-events: none;
	cursor: default;
}
```

**禁止用户选择**

```css
.wrap {
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
```

**cursor属性**

```css
.wrap {
  cursor：pointer; // 小手指；
  cursor：help; // 箭头加问号；
  cursor：wait; // 转圈圈；
  cursor：move; // 移动光标；
  cursor：crosshair; // 十字光标
}
```

**使用硬件加速**

```css
.wrap {
    transform: translateZ(0);
}
```

**图片宽度自适应**

```css
img {max-width: 100%}
```

**Text-transform和Font Variant**

```css
p {text-transform: uppercase}  // 将所有字母变成大写字母
p {text-transform: lowercase}  // 将所有字母变成小写字母
p {text-transform: capitalize} // 首字母大写
p {font-variant: small-caps}   // 将字体变成小型的大写字母
```

**将一个容器设为透明**

```css
.wrap { 
  filter:alpha(opacity=50); 
  -moz-opacity:0.5; 
  -khtml-opacity: 0.5; 
  opacity: 0.5; 
}
```

**消除transition闪屏**

```css
.wrap {
    -webkit-transform-style: preserve-3d;
    -webkit-backface-visibility: hidden;
    -webkit-perspective: 1000;
}
```

**自定义滚动条**

```css
overflow-y: scroll;
整个滚动条
::-webkit-scrollbar {
    width: 5px;
}

滚动条的轨道
::-webkit-scrollbar-track {
    background-color: #ffa336;
    border-radius: 5px;
}

滚动条的滑块
::-webkit-scorllbar-thumb {
    background-color: #ffc076;
    border-radius: 5px;
}
```

**让 HTML 识别 string 里的 '\n' 并换行**

```css
body {
  	white-space: pre-line;
}
```

**实现一个三角形**

```css
.wrap { 
  border-color: transparent transparent green transparent; 
  border-style: solid; 
  border-width: 0px 300px 300px 300px; 
  height: 0px; 
  width: 0px; 
}
```

**移除被点链接的边框**

```css
a {outline: none}
a {outline: 0}
```

**使用CSS显示链接之后的URL**

```css
a:after{content:" (" attr(href) ") ";}
```

**select内容居中显示、下拉内容右对齐**

```css
select{
    text-align: center;
    text-align-last: center;
}
select option {
    direction: rtl;
}
```

**修改input输入框中光标的颜色不改变字体的颜色**

```css
input{
    color:  #fff;
    caret-color: red;
}
```

**修改input 输入框中 placeholder 默认字体样式**

```css
//webkit内核的浏览器 
input::-webkit-input-placeholder {
    color: #c2c6ce;
}
//Firefox版本4-18 
input:-moz-placeholder {
    color: #c2c6ce;
}
//Firefox版本19+
input::-moz-placeholder {
    color: #c2c6ce;
}
//IE浏览器
input:-ms-input-placeholder {
    color: #c2c6ce;
}
```

**子元素固定宽度 父元素宽度被撑开**

```css
// 父元素下的子元素是行内元素
.wrap {
  white-space: nowrap;
}
// 若父元素下的子元素是块级元素
.wrap {
  white-space: nowrap;  // 子元素不被换行
  display: inline-block;
}
```

**让div里的图片和文字同时上下居中**

```css
.wrap {
  height: 100,
  line-height: 100
}
img {
  vertival-align：middle
}
// vertical-align css的属性vertical-align用来指定行内元素（inline）或表格单元格（table-cell）元素的垂直对齐方式。只对行内元素、表格单元格元素生效，不能用它垂直对齐块级元素
// vertical-align：baseline/top/middle/bottom/sub/text-top;
```

**实现宽高等比例自适应矩形**

```css
        .scale {
            width: 100%;
            padding-bottom: 56.25%;
            height: 0;
            position: relative; 
        }

        .item {
            position: absolute; 
            width: 100%;
            height: 100%;
            background-color: 499e56;
        }    
   <div class="scale">
        <div class="item">
            这里是所有子元素的容器
        </div>
	</div>
```

**transfrom的rotate属性在span标签下失效**

```css
span {
  display: inline-block
}
```

**边框字体同色**

```css
	.wrap {
		width: 200px;
		height: 200px;
		color: #000;
		font-size: 30px;
		border: 50px solid currentColor;
		// border: 50px solid; // 实现二
	}
```



**复选框美化**

~~~less
// 复选框
input {
  &.checkbox {
    -webkit-appearance: none;
    width: 14px !important;
    height: 14px !important;
    background: url(../img/checkbox14.png) no-repeat;
    cursor: pointer;
    &:checked {
      background: url(../img/checkboxed14.png) no-repeat;
    }
  }
}
~~~



**垂直对齐**

~~~css
.box{
    position: absolute;
    top: 50%;
    -webkit-transform: translateY(-50%);
    -o-transform: translateY(-50%);
    transform: translateY(-50%);
}
~~~

**背景渐变动画**

~~~css
button {
    background-image: linear-gradient(#5187c4, #1c2f45);
    background-size: auto 200%;
    background-position: 0 100%;
    transition: background-position 0.5s;
}    
button:hover {
    background-position: 0 0;
}
~~~

**表格列宽自适应**

~~~css
td {
    white-space: nowrap;
}
~~~

**为logo隐藏H1**

~~~css
h1 {
    text-indent: -9999px;
    margin: 0 auto;
    width: 320px;
    height: 85px;
    background: transparent url("images/logo.png") no-repeat scroll;
}
~~~

**内容垂直居中**

~~~css
.container {
    min-height: 6.5em;
    display: table-cell;
    vertical-align: middle;
} 
~~~

**CSS固定页脚**

~~~css
#footer {
    position: fixed;
    left: 0px;
    bottom: 0px;
    height: 30px;
    width: 100%;
    background: #444;
}
/* IE 6 */
* html #footer {
    position: absolute;
    top: expression((0-(footer.offsetHeight)+(document.documentElement.clientHeight ? document.documentElement.clientHeight : document.body.clientHeight)+(ignoreMe = document.documentElement.scrollTop ? document.documentElement.scrollTop : document.body.scrollTop))+'px');
}
~~~





# JavaScript

<img src="https://i.niupic.com/images/2020/02/04/6mSu.jpg" />

## 简介

> JavaScript是一门脚本语言、解释性语言、动态类型的语言、基于对象的语言

**JavaScript分为三个部分**

~~~
 1. ECMAScript 标准                 js的基本的语法
 2. DOM (Document Object Model)   	文档对象模型
 3. BOM (Browser Object Model)    	浏览器对象模型
~~~

## 变量

### 变量作用

变量是存储数据值的容器



### 变量声明

~~~js
var a; // 变量声明（注：声明之后，变量是没有值的，那么它的值是undefined）

var a = 10; // 变量声明并初始化（初始化就是赋值）
~~~

- 使用关键词 `var`，可以用来声明**局部变量**和**全局变量**。
- 直接赋值。例如`a = 10`，在函数内使用这种形式赋值，会产生一个全局变量。在严格模式下会产生错误。因此你不应该使用这种方式来声明变量。
- 使用关键词 `let` ，可以用来声明**块作用域的局部变量**。

~~~js
var a = 1;

if(a === 1) {
    var a = 2;
    console.log(a); // 2 此处a不是在函数内，所以不是局部变量，相当于重新声明的a
}

console.log(a); // 2
~~~

~~~js
function fn() {
    a = 1;   // 在函数内使用这种形式赋值，会产生一个全局变量，在严格模式（strict mode）下会抛出 ReferenceError 异常
    var b = 2;
}

fn();

console.log(a); // 1 
console.log(b); // ReferenceError: b is not defined (函数内声明的变量是局部变量，外部访问不到)

// 声明变量的作用域限制在其声明位置的上下文中，而非声明变量总是全局的
// 在函数里声明的变量是局部变量，函数外部访问不到
~~~



### 变量预解析

**预解析**

就是在浏览器解析代码之前，把**变量的声明**和**函数的声明**提前（提升）到该作用域的最上面



下面代码示例：

~~~js
console.log(a); // undefined
var a = 10;
~~~

相当于

~~~js
var a;
console.log(a); // undefined
a = 10;
~~~

提升将影响变量声明，而不会影响其值的初始化

~~~js
function fn() {
	console.log(a); // undefined
	var a = 1;
	console.log(a); // 1
}

// 相当于
function fn() {
    var a;
	console.log(a); // undefined
	var a = 1;
	console.log(a); // 1
}
~~~



### 变量作用域

在函数之外声明的变量，可被当前文档中的任何其他代码所访问，叫做**全局变量**

在函数内部声明的变量，它只能在当前函数的内部访问，叫做**局部变量**



~~~js
if (true) {
	var a = 1;
}
console.log(a); // 1
~~~

~~~js
if (true) {
	let b = 1; // let 和 const 只在块作用域有效，var没有块作用域概念
}
console.log(b); // b is not defined
~~~

~~~js
var a = 0;

function f() {
	var a = b = 1; // a在函数内部声明-是局部变量，b不是
}
f();

console.log(a, b); // 0, 1
// a 是全局变量
// b 是隐式声明的全局变量
~~~

**`注意：全局变量如果页面不关闭，那么var变量就不会释放，就会占空间，消耗内存`**



## 数据类型

### 基本数据类型

又称为简单数据类型，在内存中以固定的大小存储在栈中，按值访问

~~~js
String    Number    Boolean    undefined    null    Symbol 
字符串      数值      布尔值      未定义       空    (es6新增)
~~~



**String**

由多个16位Unicode字符组成的字符序列，用单引号或双引号表示

~~~js
var str = 'abc';
var str = '123';
~~~



**Number**

采用了IEEE754格式来表示整数和浮点数值

~~~js
var num = 10;
var num = 20;
~~~



**Boolean**

只有两个值`true`和`false`，全为小写

~~~js
var flag = true;
var flag = false;
~~~

| 数据类型  | 转为true                               | 转为false       |
| --------- | -------------------------------------- | --------------- |
| Boolean   | true                                   | false           |
| String    | 任何非空字符串                         | " "（空字符串） |
| Number    | 任何非零数字（包括无穷大），如2，-1，3 | 0和NaN          |
| Object    | 任何对象                               | null            |
| Undefined | not applicable（不适用）               | undefined       |



**null**

null 类型的值只有一个，就是null，专门用来表示一个空的对象，使用 typeof 操作符检测 null 值时会返回`object`

null 值的主要作用是如果定义的变量在将来用于保存对象，那么最好将该变量初始化为**null**值

~~~js
typeof null; // object
~~~

null不是一个对象，但为什么typeof null === object?

~~~
    这是js存在的一个悠久Bug，js的最初版本中使用的是32位系统，为了性能考虑使用低位存储变量的类型信息，在js中如果二进制的前三位都为0，就会被判断为object类型，null的二进制全为0，所以将它错误的判断为object，故 typeof null === 'object'
    也可以一句话带过：历史遗留原因，后期不改了
~~~



**undefined**

undefined 类型的值只有一个，就是undefined，表示未定义，即声明了为赋值

这个类型只有一个值，在声明变量未进行赋值时，这个变量的值就是undefined

~~~js
typeof undefined;   // undefined
~~~



### 引用数据类型

又称复杂数据类型或对象类型，存储在堆中，且大小不固定，同时在栈中会存储其指向堆地址的指针，按引用来访问

~~~js
Object    Array    Function
 对象      数组       函数
~~~



**Object**

~~~js
var obj = new Object();
~~~



**Array**

~~~js
var arr = new Array();
~~~



**Function**

~~~js
function add(a, b) {
  return a + b;
}
~~~



### 数据类型区别

**基本类型**的值是不可变得、基本类型的比较是值的比较、基本类型的变量是存放在**栈**的

**引用类型**的值是可变的、引用类型的比较是引用的比较、引用类型的值是保存在**堆**中

示例：

~~~js
var a1 = 0;
var a2 = 'this is str';
var a3 = null;
var c = [1, 2, 3];
var b = { m: 20 };
~~~



<img src="https://user-gold-cdn.xitu.io/2019/6/25/16b8c0b5752823f6?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" />

基本数据类型保存在栈内存中，因为基本数据类型占用空间小、大小固定，通过按值来访问，属于被频繁使用的数据

引用数据类型存储在堆内存中，因为引用数据类型占据空间大、占用内存不固定。 如果存储在栈中，将会影响程序运行的性能； 引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。 当解释器寻找引用值时，会首先检索其在栈中的地址，取得地址后从堆中获得实体



**栈和堆的区别**

1. 栈由系统自动分配释放，堆由程序员分配释放

2. 栈使用的是一级缓存，通常都是被调用时处于存储空间中，调用完毕立即释放；堆则是存放在二级缓存中，生命周期由虚拟机的垃圾回收算法来决定

3. 栈是一种先进后出的数据结构，堆可以被看成是一棵树



### 数据类型转换

**如何使用谷歌浏览器，快速的查看数据类型？**

字符串的颜色是`黑色`的，数值类型是`蓝色`的，布尔类型也是`蓝色`的，undefined和null是`灰色`的



在包含的数字和字符串的表达式中使用加法运算符（+），JavaScript 会把数字转换成字符串

在涉及其它运算符（译注：如下面的减号'-'）时，JavaScript语言不会把数字变为字符串

~~~js
console.log('hello' + 20); // hello30
console.log('1' + 2); // 12
console.log(1 + '2'); // 12
console.log('2' - 1); // 1
console.log(2 - '1'); // 1
~~~



#### 数值转字符串

**String()：全局方法**

把数字、文字、变量或表达式转为字符串；

有些值没有toString()，这个时候可以使用String()，比如：undefined和null

~~~js
String(3.14); // 3.14
String(1 + 2); // 3
String(true); // true
String(null); // null
String(undefined); // undefined
String(function fn() {}); // function fn() {}
String({}); // [object Object]
String([]); // ""
String(NaN); // NaN
~~~



**toString()：数字方法，不能把null和undefined转为字符串**

~~~js
(3).toString(); // 3
'hello'.toString(); // hello
true.toString(); // true
[].toString(); // ""
NaN.toString(); // NaN
~~~



~~~js
null.toString(); // Cannot read property 'toString' of null
undefined.toString(); // Cannot read property 'toString' of undefined
{}.toString(); // Uncaught SyntaxError: Unexpected token
~~~

~~~js
var b;
console.log(b.toString()); // 报错，b声明了未赋值，为undefined
var c = null;
console.log(c.toString()); // 报错
~~~



#### 字符串转数值

**Number()：全局方法，较严格**

可把字符串转换为数字，较严格

可以把任意值转换成数值，**如果要转换的字符串中有一个不是数值的字符，返回NaN**

~~~js
Number('3.14'); // 3.14
Number('11 22'); // NaN
Number(''); // 0
Number('hello'); // NaN
Number('10abc'); // NaN
Number(true); // 1
Number(false); // 0
Number(null); // 0
Number(undefined); // NaN
Number(NaN); // NaN
Number(new Date()); // 1615950656720 获取时间戳
Number({}); // NaN
Number([]); // 0
Number([1,2]); // NaN
~~~



**parseInt()**

转整数，解析一段字符串并返回数值。允许空格。只返回首个数字

~~~js
parseInt(10.5); // 10
parseInt('10.5'); // 10
parseInt('10hello'); // 10
parseInt('hello'); // NaN
parseInt('hello10'); // NaN
parseInt('10 20'); // 10
parseInt(null); // NaN
parseInt(undefined); // NaN
parseInt([]); // NaN
parseInt({}); // NaN
~~~



**parseFloat()**

转小数，解析一段字符串并返回数值。允许空格。只返回首个数字

~~~js
parseFloat(10); // 10
parseFloat(10.5); // 10.5
parseFloat('10'); // 10
parseFloat('10.5'); // 10.5
parseFloat('10.5abc'); // 10.5
parseFloat('10abc'); // 10
parseFloat('abc10'); // NaN
parseFloat(null); // NaN
parseFloat(undefined); // NaN
parseFloat([]); // NaN
parseFloat({}); // NaN
~~~



### 数据类型检测

#### typeof

**作用**

1. 使用typeof 获取变量的类型
2. typeof 来获取一个变量是否存在，变量不存在则返回 undefined



**typeof返回的数据类型**（基本数据类型使用typeof检测）

~~~js
String    Number    Boolean    undefined    Object    Function
~~~



**typeof 运算符把对象、数组或 null 返回 object，所以返回类型没有 array 和 null **

~~~js
typeof ''; // string 空的字符串变量既有值也有类型
typeof 'hello'; // string

typeof 10; // number
typeof NaN; // number

typeof true; // boolean
typeof false; // boolean

typeof undefined; // undefined
typeof a; // undefined

typeof function fn() {}; // function
typeof function() {} // function
typeof console.log // function

typeof []; // object -- 在 JavaScript 中数组即对象
typeof {}; // object
typeof null; // object -- null 是一个只有一个值的数据类型，这个值就是 null。表示一个空指针对象
typeof new Date(); // object

typeof (''); // string

typeof /[0-9]/; // object
~~~

**`注意：您无法使用 typeof 去判断 JavaScript 对象是否是数组（或日期）`**



#### instanceof

**作用：**用于判断一个变量是否属于某个对象的实例

~~~js
const a = [];
a instanceof Array; // true
// a.__proto__ == Array.prototype
~~~

~~~js
1. 只要在当前实例的原型链上，用 instanceof 检测出来的结果都是 true，所以在类的原型继承中，最后检测出来的结果未必是正确的，而且 instanceof 后面必须跟一个对象
2. 不能检测基本类型
~~~





#### 检测数组

**constructor 属性**
constructor 属性返回所有 JavaScript 变量的构造器函数

每个构造函数的原型对象都有一个constructor属性，并且指向构造函数本身，由于我们可以手动修改 这个属性，所以结果也不是很准确。 不能检测null和undefined

~~~js
"hello".constructor                     // 返回 "function String()  { [native code] }"
(3.14).constructor                      // 返回 "function Number()  { [native code] }"
false.constructor                       // 返回 "function Boolean() { [native code] }"
[1, 2, 3, 4].constructor                // 返回 "function Array()   { [native code] }"
{ name: 'hello', age: 20 }.constructor  // 返回" function Object()  { [native code] }"
new Date().constructor                  // 返回 "function Date()    { [native code] }"
function () {}.constructor              // 返回 "function Function(){ [native code] }"
~~~

您可以通过检查 constructor 属性来确定某个对象是否为数组（包含单词 "Array"）

~~~js
function isArray(arr) {
    return arr.constructor.toString().indexOf('Array') > -1;
}
~~~

您可以通过检查 constructor 属性来确定某个对象是否为日期（包含单词 "Date"）

~~~js
function isDate(date) {
    return date.constructor.toString().indexOf('Date') > -1;
}
~~~



**Object.prototype.toString.call（检测数组最佳方案）**

调用Object原型上的toString()方法，并且通过call改变this指向，返回的是字符串

~~~js
function isArray(arr) {
	return Object.prototype.toString.call(arr) === '[object Array]';
}
~~~



**ES6方法Array.isArray()**

~~~js
const arr = [];
Array.isArray(arr); // true
~~~



### **NaN 和 isNaN()**

**NaN**

NaN（Not a Number)，即非数值，用于表示一个本来要返回数值的操作数未返回数值的情况

特点：

~~~js
1. 任何涉及NaN的操作 (例如 NaN/10) 都会返回NaN
2. NaN与任何值都不相等，包括NaN本身
~~~



**isNaN()函数**

这个函数接受一个参数，该参数可以是任何类型。isNaN()在接收到一个值后，会尝试将这个值转换为数值，而任何不能被转换为数值的值都会导致函数返回true

~~~js
isNaN(NaN); // true 
isNaN(10); // false（10 是一个数值）
isNaN("10"); // false（可以被转换成数值 10）
isNaN("blue"); // true（不能转换成数值）
isNaN(true); // false（可以被转换成数值 1）
~~~



## 运算符

### 算数运算符

| 运算符 | 描述 |
| :----- | :--- |
| +      | 加法 |
| -      | 减法 |
| *      | 乘法 |
| /      | 除法 |
| %      | 系数 |
| ++     | 递加 |
| --     | 递减 |



~~~js
var a = 10 + 20; // 30
var a = '20' + '10'; // 2010
var a = '20' + 10; // 2010
var a = 10 + '20'; // 1020
var a = 10 + NaN; // NaN
var a = NaN + 10; // NaN
var a = '10' + NaN; // 10NaN
var a = NaN + '10'; // NaN10
var a = undefined + 10; // NaN
var a = true + 0; // 1
var a = {} + [];  // 0
var a = 1 + {};  // 1[object Object]
var a = 1 + [];  // 1
var a = 1 + [2];  // 12
1 + [2, 3]; // 12,3

var b = 20 - 10; // 10
var b = 20 - '10'; // 10
var b = '20' - 10; // 10
var b = '20' - '10'; // 10
var b = 10 - NaN; // NaN
var b = NaN - 10; // NaN
var b = '10' - NaN; // NaN
var b = NaN - '10'; // NaN

var c = 10 * 20; // 200
var c = '10' * 20; // 200
var c = 10 * '20'; // 200
var c = 10 * NaN; // NaN
var c = NaN * 10; // NaN
var c = '10' * NaN; // NaN
var c =  NaN * '10'; // NaN
var c = null * 10; // 0  空值null在数值类型环境中会被当作0来对待，而布尔类型环境中会被当作false
var c = true * 10; // 10
var c = false * 10; // 0

var d = 20 / 10; // 2
var d = '20' / 10; // 2
var d = 20 / '10'; // 2
var d = NaN / 10; // NaN
var d = 10 / NaN; // NaN
var d = '10' / NaN; // NaN
var d  = NaN / '10'; // NaN
~~~

~~~js
var a = 10;
var b = 20;
var c = 4;
console.log(++b+c+a++); // 21 + 4 + 10 = 35
~~~

~~~js
var a = '11' + 2 - '1';
console.log(a); // 111
console.log(typeof a); // number
~~~



### 赋值运算符

| 运算符 | 例子   | 等同于    |
| :----- | :----- | :-------- |
| =      | x = y  | x = y     |
| +=     | x += y | x = x + y |
| -=     | x -= y | x = x - y |
| *=     | x *= y | x = x * y |
| /=     | x /= y | x = x / y |
| %=     | x %= y | x = x % y |

### 比较运算符

| 运算符 | 描述           |
| :----- | :------------- |
| ==     | 等于           |
| ===    | 等值等型       |
| !=     | 不相等         |
| !==    | 不等值或不等型 |
| >      | 大于           |
| <      | 小于           |
| >=     | 大于或等于     |
| <=     | 小于或等于     |
| ?      | 三元运算符     |

`==`会自动转换类型，然后再比较，`===`不会类型转换，直接比较

~~~js
1 == 1; // true
1 == '1'; // true
1 == true; // true
0 == false; // true
2 == true; // false
0 == ''; // true
[] == 0;  // true
![] == 0;  // true
[] == ![];  // true
[] == [];  // false
[] == false; // true
{} == {};  // false
{} == !{}; // false
NaN == NaN; // false
undefined == null // true
undefined === null // false

1 === 1; // true
1 === '1'; // false
1 === true; // false
[] === 0  // false
=== // 先判断左右两边的数据类型，如果数据类型不一致，直接返回 false，之后才会进行两边值的判断

'1' < '2'; // true
'1' < 2; // true
'1' > '2'; // false
'1' > 2; // false

null == null; // true
null === null; // true

undefined == undefined; // true
undefined === undefined; // true

null == undefined; // true
null === undefined; // false

!null; // true
isNaN(1 + null); // false  (1 + null = 1 + 0 = 1, null在数值环境转为0) 
isNaN(1 + undefined); // true (1 + undefined = 1 + NaN = 1, undefined在数值环境转为NaN)

NaN == NaN; // false
NaN === NaN; // false
~~~



### 逻辑运算符

| 运算符 | 描述   |
| :----- | :----- |
| &&     | 逻辑与 |
| \|\|   | 逻辑或 |
| !      | 逻辑非 |

**示例**

~~~js
true || false // true

true && false // false
~~~



~~~js
'hello'; // hello
!'hello'; // false
!!'hello'; // true
~~~



## 对象

### 简介

**对象：**有`属性`和`方法`，具体特指的某个事物

~~~js
var obj = {
    name: '张三',
    sayHello: function() {
        console.log('hello');
    }
}
// 上面定义了一个普通对象obj
// name 是属性
// sayHello 是方法，方法的定义：当一个函数是一个对象的属性时，称之为方法
~~~

在 JavaScript 中，几乎“所有事物”都是对象。

- 布尔是对象（如果用 *new* 关键词定义）
- 数字是对象（如果用 *new* 关键词定义）
- 字符串是对象（如果用 *new* 关键词定义）
- 日期永远都是对象
- 算术永远都是对象
- 正则表达式永远都是对象
- 数组永远都是对象
- 函数永远都是对象
- 对象永远都是对象

所有 JavaScript 值，除了原始值，都是对象

~~~js
// JavaScript 原始值：指的是没有属性或方法的值
string    number    boolean    null    undefined
~~~

~~~js
对象是包含变量的变量，对象也是变量
方法是可以在对象上执行的动作
~~~

Javascript中的对象包括：**自定义对象、内置对象、浏览器对象**

### 对象创建

**字面量创建对象**

注意：方法里的this指向当前对象，能被当前对象直接调用

```js
var obj = {
  name: 'web',
  age: 20,
  sayName: function() {
    console.log('my name is ' + this.name); // 这里this指向当前对象
  }
}
obj.sayName(); // my name is web
```

```js
var obj = {};
obj.name = 'web';
obj.age = 20;
obj.sayName = function() {
  console.log('my name is ' + this.name);
}
obj.sayName() // my name is web
```



**自定义构造函数创建对象**

注意：构造函数里的this指向当前new出来的实例对象，能被实例对象直接调用

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.getInfo = function() {
    console.log('my name is ' + this.name + ', my age is ' + this.age);
  }
}

// 创建对象
var obj = new Person('Jack', 20);
obj.name; // Jack
obj.age; // 10
obj.getInfo(); // my name is Jack, my age is 20
```



**new Object()创建对象**

```js
var person = new Object();

person.name = 'Jack';
person.age = 20;
person.sayHi = function(){
  console.log('hello');
}
```



**工厂方法创建对象**

```js
function createPerson(name, age) {
  var person = new Object();
  person.name = name;
  person.age = age;
  person.sayHi = function() {
    console.log('hello');
  }
  return person;
}
var p = createPerson('Jack', 20);
```



### 对象调用

**设置和获取属性**

```js
对象属性的调用：obj.name    obj['name']
对象的方法调用：obj.sayHello();
```

```js
var obj = {
  name: 'Jack',
  age: 20,
  sayHello: function() {
    console.log('hello');
  }
}

// 属性的调用
obj.name; // Jack
obj['name']; // Jack

// 设置属性值
obj['name']; = 'Mark';
obj['name']; // Mark

// 方法的调用
obj.sayHello(); // hello
obj['sayHello'](); // hello
```



**obj.attr 与obj['attr'] 的区别**

~~~js
// []可以用变量作为属性名访问，而点不行
// []可以用数字作为属性访问，但点不行
// []可以动态访问属性名，可以在程序运行时创建和修改
~~~



### 对象遍历

通过for..in语法可以遍历一个对象

```js
for(var key in obj) {
  console.log(key + "==" + obj[key]);
}
```

**删除对象属性**

```js
delete obj.name;
```



### 对象易变

对象是易变的：它们通过引用来寻址，而非值，对象存储在堆中

**注释：**JavaScript 变量不是易变的。只有 JavaScript 对象如此

~~~js
var b = {
  name: 'hi'
}
var a = b; // 此时只是把引用地址给了a， a和b是同一个对象（所以改变a，同时也会改变b）
a.name = 'hello';
b; // { name: 'hello' }
~~~



### 内置对象

内置对象：JS系统自带的对象

~~~js
Math    Date    String    Array    Object    JSON
~~~

#### Number对象

| 方法                | 说明                                                         |
| ------------------- | ------------------------------------------------------------ |
| Number.parseInt()   | 把字符串解析成特定基数对应的整型数字，和全局方法 parseInt() 作用一致 |
| Number.parseFloat() | 把字符串参数解析成浮点数，<br/>和全局方法 parseFloat() 作用一致 |

**数字类型原型上的一些方法**

| 方法            | 说明                                                         | 示例                                      |
| --------------- | ------------------------------------------------------------ | ----------------------------------------- |
| toFixed()       | 返回指定小数位数的表示形式                                   | var a=123,b=a.toFixed(2) //b="123.00"     |
| toExponential() | 返回一个数字的指数形式的字符串                               | 1.23e+2                                   |
| toPrecision()   | 返回一个指定精度的数字。如下例子中，a=123中，3会由于精度限制消失 | var a=123,b=a.toPrecision(2) //b="1.2e+2" |



#### Math对象

| 方法               | 说明       | 示例                                                         |
| ------------------ | ---------- | ------------------------------------------------------------ |
| Math.floor(值)     | 向下取整   | Math.floor(12.3)=12；Math.floor(12.9)=12；                   |
| Math.ceil(值)      | 向上取整   | Math.floor(12.3)=13；Math.floor(12.9)=13；                   |
| Math.abs(值)       | 绝对值     | （-1=1、-2=2、null=0、”string”=NaN）                         |
| Math.round(值)     | 四舍五入   | Math.floor(12.3)=12；Math.floor(12.5)=13；                   |
| Math.max(一组数值) | 取最大值   | Math.max(3, 2, 5, 6)=6                                       |
| Math.min(一组数值) | 取最小值   | Math.max(3, 2, 5, 6)=2                                       |
| Math.power(2,4)    | 求指数次幂 | 16                                                           |
| Math.sqrt(16)      | 求平方根   | 4                                                            |
| Math.sin( )        | 正弦       |                                                              |
| Math.cos( )        | 余弦       |                                                              |
| Math.random( )     | 生成随机数 | parseInt(Math.random()*5)+1;<br />//0~4随机数（其中Math.random()产生0.0~1.0之间的随机double值） |
| Math.PI            | 圆周率     |                                                              |



#### Date对象

~~~js
let date = new Date().toISOString().slice(0, 10) // 获取当前日期：格式为'2020-05-20'
~~~



```js
var d = new Date()
console.log(d) // Sun Apr 14 2019 20:46:02 GMT+0800 (中国标准时间)
dt.valueOf() // 毫秒1555246148513

var d = Date.now()
console.log(d) // 毫秒1555246148513
```

```js
var d = new Date()

d.getFullYear() // 获取年份
d.getMonth() + 1 // 获取月份，是0开始的 真实的月份是需要加1的
d.getDate() // 获取日期
d.getHours() // 获取小时
d.getMinutes() // 获取分钟 
d.getSeconds() // 获取秒
d.getDay() //0获取星期，星期从0开始的
```

```js
function getNowTime() {
	var date = new Date();
	h = date.getHours();
	m = date.getMinutes();
	s = date.getSeconds();
	hou = (h < 10 ? "0" : "") + h;
	min = (m < 10 ? "0" : "") + m;
	sec = (s < 10 ? "0" : "") + s;
	var ymd = date.getFullYear() + '-' + (date.getMonth() + 1) + '-' + date.getDate() + " " + hou + ':' + min + ':' + sec;
	w = date.getDay();
	week = "星期" + "日一二三四五六".split('')[w];
	var nowdate = ymd + " " + week;
	document.getElementById("time").innerHTML = nowdate;
}
setInterval("getNowTime()", 1000);
```

**秒杀倒计时**

~~~js
function getTime() {
    var startTime = '2020-05-28 09:00:00';
    var endTime = '2020-05-28 12:00:00';
    var nowTime = new Date().getTime() - new Date(startTime).getTime() >= 0 ? new Date().getTime() : new Date(startTime).getTime();
    var time = new Date(endTime).getTime() - nowTime;
    time = time / 1000;
    var d = {
        h: Math.floor(time / 3600) < 10 ? '0' + Math.floor(time / 3600) : Math.floor(time / 3600),
        m: Math.floor(time % 3600 / 60) < 10 ? '0' + Math.floor(time % 3600 / 60) : Math.floor(time % 3600 / 60),
        s: Math.floor(time % 3600 % 60) < 10 ? '0' + Math.floor(time % 3600 % 60) : Math.floor(time % 3600 % 60)
    }
    console.log(`${d.h}-${d.m}-${d.s}`)
}

setInterval(() => {
    getTime()
}, 500);
~~~



#### String对象



#### Array对象

**Array()**

~~~js
Array(); // []
Array(3); // [, , ,]
Array(1, 2, 3); // [1, 2, 3]
Array(undefined); // [undefined]
~~~



**Array.of()**

方法用于将一组值，转换为数组（ES6）

~~~js
Array.of(); // []
Array.of(3); // [3]
Array.of(1, 2, 3); // [1, 2, 3]
Array.of(undefined) // [undefined]
~~~



**Array.from()**

方法用于将两类对象转为真正的数组（ES6）

~~~js
Array.from('hello');
// ['h', 'e', 'l', 'l', 'o']

Array.from([1, 2, 3]);
// [1, 2, 3]
~~~



#### Object对象

**Object.assign(target, source)**

注意：会改变目标对象target

~~~js
const a = { a: 1, b: 2 };
const b = { b: 3, c: 5 };

const c = Object.assign(a, b);

console.log(a); // { a: 1, b: 3, c: 5 }

console.log(c); // { a: 1, b: 3, c: 5 }
~~~



**Object.prototype.hasOwnProperty()**

方法会返回一个布尔值，指示对象自身属性中是否具有指定的属性（也就是，是否有指定的键）

~~~js
var obj = { a: 10, b: 20, c: 30 };
obj.hasOwnProperty('a'); // true
obj.hasOwnProperty('d'); // false
~~~

~~~js
var arr = [1, 2, 3];
arr.hasOwnProperty(0); // true
arr.hasOwnProperty(1); // true
arr.hasOwnProperty(2); // true
arr.hasOwnProperty(3); // false
~~~





#### JSON对象

**JSON**(JavaScript Object Notation) 是一种轻量级的数据交换格式。

它是基于JavaScript的一个子集，数据格式简单，易于读写，占用宽带小



JSON格式的数据：一般都是成对的，是键值对，json也是一个对象，数据都是成对的，一般json格式的数据无论是键还是值都是用双引号括起来的

```js
var json = {
	"name": "Jack",
	"age": "10",
	"sex": "man"
}
```

**JSON.stringify()**

```js
// 服务器接受到的数据永远是字符串，故发送到服务器的数据是对象JSON字符串化
JSON.stringify({a:10, b:20}) 
```

**JOSN.parse()**

~~~js
// 从服务器获取的数据永远是字符串，故需解析为JS对象化
JOSN.parse('{"a":10,"b":20}') 
~~~

**JSON遍历**

遍历对象，是不能通过for循环遍历，无序，key是一个变量，这个变量中存储的是该对象的所有的属性的名字

```js
for (var key in json) {
	console.log(key + "--" + json[key])
}

// name--Jack
// age--10
// sex--man
```



### getters 与 setters

一个 getter 是一个获取某个特定属性的值的方法

一个  setter 是一个设定某个属性的值的方法

~~~js
var obj = {
  a: 7,
  get b() { 
    return this.a + 1;
  },
  set c(x) {
    this.a = x / 2
  }
};

console.log(obj.a); // 7
console.log(obj.b); // 8
obj.c = 50;
console.log(obj.a); // 25
console.log(obj.b); // 26
~~~



### ES5 新的对象方法

~~~js
// 添加或更改对象属性
Object.defineProperty(object, property, descriptor)

// 添加或更改多个对象属性
Object.defineProperties(object, descriptors)

// 访问属性
Object.getOwnPropertyDescriptor(object, property)

// 以数组返回所有属性
Object.getOwnPropertyNames(object)

// 以数组返回所有可枚举的属性
Object.keys(object)

// 访问原型
Object.getPrototypeOf(object)

// 阻止向对象添加属性
Object.preventExtensions(object)

// 如果可将属性添加到对象，则返回 true
Object.isExtensible(object)

// 防止更改对象属性（而不是值）
Object.seal(object)

// 如果对象被密封，则返回 true
Object.isSealed(object)

// 防止对对象进行任何更改
Object.freeze(object)

// 如果对象被冻结，则返回 true
Object.isFrozen(object)
~~~



## 字符串

### 字符串简介

用于存储和操作文本



**字符串长度**

内建属性 length 可返回字符串的长

~~~js
var str = 'hello';
str.length; // 5
~~~



**字符串可以是对象**

通常，JavaScript 字符串是原始值，通过字面方式创建

~~~js
var a = 'hello';
typeof a; // string
~~~

但是字符串也可通过关键词 new 定义为对象

~~~js
var b = new String("hello");
b; // String {"hello"}
typeof b; // object
~~~

上面两个对象值相等，但类型不相同，因此

~~~js
a == b; // true
a === b; // false 因为a是字符串，b是对象
~~~

**`对象无法比较`**

~~~js
var a = new String("hello");
var b = new String("hello");
a == b; // false
~~~

~~~js
var a = {};
var b = {};
a == b; // false
~~~



### 字符串方法

​		字符串可以看成是字符组成的数组，但是js中没有字符类型，在js中字符串可以使用单引号也可以使用双引号，因为字符串可以看成是数组，所以可以通过for循环进行遍历

字符串特性：不可变性，字符串的值是不能改变



**`length`** 

属性返回字符串的长度

```js
var str = 'abcde';

console.log(str.length); // 5
```



**`indexOf(字符串)`** 

方法返回字符串中指定文本**首次出现**的索引位置，没找到返回-1

```js
var str = '12345678988';

var index = str.indexOf('8', 5); // 7
var index = str.indexOf('10', 5); // -1 没有返回-1
```



**`concat()`** 

字符串拼接合并，连接两个或更多字符串，并返回新的字符串 【不改变原有字符串】

```js
var str1 = '123';
var str2 = '456';
var a = str1.concat(str2);
a // 123456

var str1 = 'a';
var str2 = 'b';
var str3 = 'c';
var a = str1.concat(str2, str3);
a // abc
```



**`replace()`** 

字符串替换，默认替换第一个 【不改变原字符串】

~~~js
var str = 'aaabbccc';

str.replace('b', 'e'); // aaaebccc
~~~



**`split()`** 

把字符串分割为字符串数组 【不改变原字符串】

```js
// 字符串转数组
var str = 'A,B,C';
var arr = str.split(',');
arr // ["A", "B", "C"]

// 数组转字符串
var arr = ['A','B','C'];
var str = arr.join(',');
str // A,B,C
```



**`includes`**  

判断字符串中是否包含指定的子字符串 【不改变原字符串】

~~~js
var str = 'hello, today is goods';

str.includes('is'); // true
str.includes('no'); // false
~~~



**`slice(起始索引,  终止索引-1)`** 

截取字符串，如果省略第二个参数，则截取字符串剩余部分 【不改变原字符串】

```js
var str = '123456789a';

str.slice(3); // 456789a 
str.slice(5, 7); // 67
```



**`substr(起始索引,  长度)`** 

返回的是截取后的新的字符串【不改变原字符串】

```js
var str = '123456789';

str.substr(5); // 6789
str.substr(5, 3); // 678
str; // 123456789
```



**`trim()`** 

干掉字符串两端的空格 【不改变原字符串】

```js
var str = '  a  b  c  ';

str.trim(); // a b c
str; // '  a  b  c  '
```



**`toLowerCase() / toUpperCase()`** 

转小写/转大写【不改变原字符串】

~~~js
var str = 'AaBbCc';

str.toLowerCase(); // aabbcc
str.toUpperCase(); // AABBCC
str; // AaBbCc
~~~



## 数组

### 数组简介

数组：**是一种特殊的变量，它能够一次存放一个以上的值；一组有序的数据**

作用：**用于在单一变量中存储多个值**

**`注意：数组是一种特殊类型的对象`**



### 数组创建

**通过字面量的方式创建数组（推荐）**

```js
var arr = []; // 空数组
var arr = [1, 2, 3, 4, 5];
```

数组长度

~~~js
var arr = [1, 2, 3, 4, 5];
arr.length; // 5
~~~

访问元素（通过索引访问）

~~~js
var arr = [5, 3, 2, 4, 1];
arr[0]; // 5
arr[1]; // 3
arr[5]; // undefined
~~~

数组赋值

```js
// 如果下标有对应的值，会把原来的值覆盖，如果下标不存在，会给数组新增一个元素。
var arr = [3,1,2];
arr[0] = 5;
arr; // [5, 1, 2]
arr[3] = 6;
arr; // [5, 1, 2, 6]
```



**通过构造函数创建数组**

```js
var arr = new Array(); // 空数组
var arr = new Array(5); // 定义了一个长度为5的空数组
var arr = new Array(1,2,4,3,5); // 定义了一个数据为[1,2,3,4,5]的数组
```

~~~js
// 能通过构造函数创建，证明数组也是对象
var arr = new Array(1,2,4,3,5);

typeof arr; // object
arr instanceof Array; // true
arr instanceof Object; // true
~~~



### 数组方法

| 序号 | 方法       | 描述                                                         |
| ---- | ---------- | ------------------------------------------------------------ |
| 6    | concat()   | 连接（合并）两个或更多的数组，并新的数组，**不改变原数组**   |
| 7    | reverse()  | 反转数组                                                     |
| 8    | splice()   | 通过索引删除某个元素，或插入元素                             |
| 9    | slice()    | 1. 复制一个数组        2.截取数组的的一部分，并返回一个新数组，**不改变原数组** |
| 10   | sort()     | 数组排序，**会改变原数组**                                   |
| 11   | reduce()   | 将数组元素计算为一个值（从左到右）                           |
| 12   | indexOf()  | 找出某个元素在数组中的索引，没找到这个元素就返回-1           |
| 13   | valueOf()  | 返回数组对象的原始值                                         |
| 14   | toString() | 把数组转换为字符串，并返回结果                               |
| 15   | forEach()  | 数组每个元素都执行一次回调函数                               |
| 16   | map()      | 通过指定函数处理数组的每个元素，并返回处理后的数组      方法返回一个由原数组中的每个元素调用一个指定方法后的返回值组成的新数组，**不改变原数组** |
| 17   | filter()   | 过滤数组，并返回符合条件的所有元素组成新的数组，**不改变原数组** |
| 18   | every()    | 检测数值元素的每个元素是否都符合条件，**不改变原数组**       |
| 19   | some()     | 检测数组元素中是否有元素符合指定条件，**不改变原数组**       |



**push()**

向数组末尾添加一个新的元素或更多元素，并返回新的长度

~~~js
var arr = [1, 2, 3];
arr.push(4);
console.log(arr); // [1, 2, 3, 4]
~~~

~~~js
var arr = [1, 2, 3];
var len = arr.push(4, 5);
console.log(arr); // [1, 2, 3, 4, 5]
console.log(len); // 5 返回长度
~~~



**pop()**

删除数组最后一个元素，并返回删除的元素，如果数组为空返回undefined

~~~js
var arr = [1, 2, 3];
arr.pop();
console.log(arr); // [1, 2]
~~~

~~~js
var arr = [1, 2, 3];
var ele = arr.pop();
console.log(arr); // [1, 2]
console.log(ele); // 3 返回删除的元素
~~~

~~~js
var arr = [];
arr.pop(); // undefined
~~~



**unshift()**

向数组开头添加一个新的元素或更多元素，并返回新的长度

~~~js
var arr = [1, 2, 3];
arr.unshift(0);
console.log(arr); // [0, 1, 2, 3]
~~~

~~~js
var arr = [1, 2, 3];
var len = arr.unshift(6, 9);
console.log(arr); // [6, 9, 1, 2, 3]
console.log(len); // 5 返回长度
~~~



**shift()**

删除数组第一个元素，并返回删除的元素，如果数组为空返回undefined

~~~js
var arr = [1, 2, 3];
arr.shift();
console.log(arr); // [2, 3]
~~~

~~~js
var arr = [1, 2, 3];
var ele = arr.shift();
console.log(arr); // [2, 3]
console.log(ele); // 1
~~~

~~~js
var arr = [];
arr.shift(); // undefined
~~~



**reverse()**

反转数组 【改变原数组】

~~~js
var arr = [1, 2, 3];
arr.reverse();
arr; // [3, 2, 1]
~~~



**splice(删除元素的索引,  删除元素数量,  新插入的元素)**

第一个参数是索引，通过索引删除数组元素【改变原数组】

~~~js
var arr = [1, 2, 3];
arr.splice(2);
arr; // [1, 2]
~~~

第二个参数是删除元素个数，如果设置为 0，则不会删除项目

~~~js
var arr = [1, 2, 3];
arr.splice(0, 2);
arr; // [3]
~~~

第三个参数是新插入的元素

~~~js
var arr = [1, 2, 3];
arr.splice(1, 0, 4);
arr; // [1, 4, 2, 3]  插入元素
~~~



**join()**

数组转字符串，【不改变原数组】

~~~js
var arr = [1, 2, 3];

arr.join('-'); // 1-2-3
arr; // [1, 2, 3]
~~~



**concat()**

连接（合并）两个或更多的数组，并新的数组【不改变原数组】

~~~js
var arr1 = [1, 2, 3];
var arr2 = [3, 4, 5];
var a = arr1.concat(arr2);
a; // [1, 2, 3, 3, 4, 5] 	必须声明一个变量接受返回数据
~~~

~~~js
var arr1 = [1, 2];
var arr2 = [3, 4];
var arr3 = [5, 6];
var a = arr1.concat(arr2, arr3);
a; // [1, 2, 3, 4, 5, 6]
~~~

ES6语法

~~~js
var arr1 = [1, 2];
var arr2 = [3, 4];
var arr3 = [5, 6];
var a = [...arr1, ...arr2, ...arr3];
a; // [1, 2, 3, 4, 5, 6]
~~~



**slice()**

复制数组【不改变原数组】

~~~js
var arr = [1, 2, 3];
var copyArr = arr.slice();
copyArr; // [1, 2, 3]
~~~

截取数，两个参数都是索引

~~~js
var arr = [1, 2, 3, 4, 5, 6];
var newArr = arr.slice(1, 3);
newArr; // [2, 3]
~~~



**sort()**

对数字进行排序（推荐）

~~~js
var arr = [1, 6, 2, 4, 3, 5];
var a = arr.sort((a, b) => a - b);
arr; // [1, 2, 3, 4, 5, 6]
a; // [1, 2, 3, 4, 5, 6]
~~~

完整写法

~~~js
var arr = [1, 6, 2, 5, 3];

arr.sort(function(a, b) {
	if(a > b) {
		return 1
	} else if(a == b) {
		return 0
	} else {
		return -1
	}
})

arr; // [1, 2, 3, 5, 6]
~~~

对包含对象的数组排序

~~~js
var arr = [
    {id: 001, sortNo: 2, name: 'c'},
    {id: 002, sortNo: 1, name: 'a'},
    {id: 003, sortNo: 3, name: 'b'}
];

// sort by sortNo
arr.sort(function(a, b) {
  return (a.sortNo - b.sortNo)
})

0: {id: 2, sortNo: 1, name: "a"}
1: {id: 1, sortNo: 2, name: "c"}
2: {id: 3, sortNo: 3, name: "b"}

--------------------------------

// sort by name
arr.sort(function(i, j) {
  var a = i.name.toUpperCase();
  var b = j.name.toUpperCase();
  if(a > b) {
    return 1;
  }
  if(a < b) {
    return -1;
  }
  return 0;
})

0: {id: 2, sortNo: 1, name: "a"}
1: {id: 3, sortNo: 3, name: "b"}
2: {id: 1, sortNo: 2, name: "c"}
~~~

示例封装方法

~~~js
var arr = [
    {id: 001, sortNo: 2, name: '小二'},
    {id: 002, sortNo: 1, name: '小一'},
    {id: 003, sortNo: 3, name: '小三'}
];
  
function objArrSort(key) {
	return function(i, j) {
		var a = i[key];
		var b = j[key];
		if(a > b) {
			return 1;
         } else if(a == b) {
			return 0;
		} else {
  	  		return -1;
  		}
    }
}
  
var sortArr = arr.sort(objArrSort('sortNo'))
console.log(sortArr)

0: {id: 2, sortNo: 1, name: "小一"}
1: {id: 1, sortNo: 2, name: "小二"}
2: {id: 3, sortNo: 3, name: "小三"}
~~~



**reduce()**

将数组元素计算为一个值（从左到右）

~~~js
arr.reduce(callback, [initialValue])

callback(acc, cur, idx, arr) // (累计器, 当前值, 当前索引, 源数组)

[initialValue] // 作为第一次调用 callback 的第一个参数
~~~

~~~js
var arr = [1, 2, 3, 4]
var sum = arr.reduce((acc, cur, idx, arr) => {
    console.log(acc, cur, idx)
    return acc + cur
})
console.log(arr, sum)
~~~

~~~js
1 2 1
3 3 2
6 4 3
[1, 2, 3, 4] 10
~~~

这里可以看出，上面的例子index是从1开始的，第一次的acc的值是数组的第一个值。数组长度是4，但是reduce函数循环3次

reduce的简单用法

~~~js
var  arr = [1, 2, 3, 4];
var sum = arr.reduce((x, y) => x + y)
var mul = arr.reduce((x, y) => x * y)
console.log( sum ) // 10 求和
console.log( mul ) // 24 求乘积
~~~

reduce的高级用法

（1）计算数组中每个元素出现的次数

```js
var arr = ['a', 'b', 'c', 'd', 'b', 'b'];

var a = arr.reduce((pre, cur) => {
  if(cur in pre){
    pre[cur]++
  }else{
    pre[cur] = 1 
  }
  return pre
}, {})
console.log(a) // {a: 1, b: 3, c: 1, d: 1}
```

（2）数组去重

```js
var arr = [1, 2, 3, 4, 3]
var a = arr.reduce((pre, cur)=>{
    if(!pre.includes(cur)){
      return pre.concat(cur)
    }else{
      return pre
    }
}, [])
console.log(a) // [1, 2, 3, 4]
```

（3）将二维数组转化为一维

```js
var arr = [[0, 1], [2, 3], [4, 5]]
var a = arr.reduce((pre, cur)=>{
    return pre.concat(cur)
}, [])
console.log(a) // [0, 1, 2, 3, 4, 5]
```

（3）将多维数组转化为一维

```js
var arr = [[0, 1], [2, 3], [4, [5, 6, 7]]]
var fn = function(arr){
   return arr.reduce((pre, cur) => pre.concat(Array.isArray(cur) ? fn(cur) : cur), [])
}
console.log(fn(arr)) // [0, 1, 2, 3, 4, 5, 6, 7]
```

（4）对象里的属性求和

```js
var arr = [
	{ num: 2, price: 0.1 },
	{ num: 3, price: 0.2 },
	{ num: 1, price: 0.3 }
]

var sum = arr.reduce((prev, cur) => {
    return cur.price + prev
}, 0)
console.log(sum) // 0.6000000000000001
```



**indexOf()**

找出某个元素在数组中的索引，没找到这个元素就返回-1

~~~js
var arr = [1, 2, 3];
var a = arr.indexOf(3); // 2
var b = arr.indexOf(4); // -1    没找到这个元素就返回-1，也就是数组不存在这个元素
~~~



**isArray()**

判断对象是不是数组类型: 两种

~~~js
var arr = [1, 2, 3];

console.log(arr instanceof Array); // true
console.log(Array.isArray(arr)); // true
~~~



**forEach()**

遍历数组用，相当于for循环

```js
var arr = [1, 2, 3];
arr.forEach((item, index, array) => {
  console.log(item, index, array)
})

结果：
1 0 [1, 2, 3]
2 1 [1, 2, 3]
3 2 [1, 2, 3]

// 第一个参数：item 当前元素
// 第二个参数：index 当前元素索引
// 第三个参数：array 数组本身
```



**map()**

方法返回一个由原数组中的每个元素调用一个指定方法后的返回值组成的新数组，不改变原数组

~~~js
var arr = [1, 2, 3];
var res = arr.map((item, index, array) => {
    return item + 1;
})
console.log(res) // [2, 3, 4]  返回新数组
console.log(arr) // [1, 2, 3]  不改变原数组

// 第一个参数：item 当前元素，必须
// 第二个参数：index 当前元素索引，可选
// 第三个参数：array 数组本身，可选
~~~



> p是普通价格，l是一个数组，里面有3个阶梯价格，如果有阶梯价格就不显示普通价格，显示阶梯价格最小的价格

~~~js
p:20
l:[{price:10},{price:30},{price:20}]
~~~

~~~js
getPrice(p, l) {
  if (l) {
    return Math.min.apply(null, l.map(x => parseFloat(x.price)))
  } else {
      return p
  }
}
~~~



**filter()**

过滤数组，并返回符合条件的所有元素组成新的数组，不改变原数组，**`filter() 不会对空数组进行检测 `**

~~~js
var arr = [1, 2, 3];
var res = arr.filter((item, index, array) => {
    console.log(item, index, array);
})

// 1 0 [1, 2, 3]
// 2 1 [1, 2, 3]
// 3 2 [1, 2, 3]

// 第一个参数：item 当前元素
// 第二个参数：index 当前元素索引
// 第三个参数：array 数组本身
~~~

filter() 不会对空数组进行检测

~~~js
var arr = [];
var res = arr.filter(i => i);
res; // []
~~~

~~~js
var arr = [1, 2, 3];
var res = arr.filter(item => item > 1);
res; // [2, 3]
~~~

删掉数组中的空字符串

~~~js
var arr = ['a', 'b', ''];
var res = arr.filter(item => {
	return item && item.trim(); // 注意：IE9以下的版本没有trim()方法，Number类型没有trim()方法
})
res; // ["a", "b"]
~~~

filter实现数组去重

~~~js
var arr = ['a', 'b', 'b', 'c', 'b']
var res = arr.filter((item, index, array) => {
	return array.indexOf(item) === index
})
console.log(res) // ["a", "b", "c"]
~~~



**every()**

方法是js中的迭代方法，用于检测数组中的**所有元素**是否满足指定条件

* 依次执行数组元素，如果一个元素不满足条件就返回false，不会继续执行后面的元素判断；所有数组元素都满足条件则返回true
* 不会改变原数组

~~~js
var arr = [1, 2, 3, 4, 5, 6];

var a = arr.every(function( item, index, array) {
    console.log(item); // 打印1，不会打印2、3、4、5、6
    return item > 4;
})

a; // false
~~~

~~~js
var arr = [1, 2, 3, 4, 5, 6];

var a = arr.every(function( item, index, array) {
    console.log(item); // 打印 1、2、3、4、5、6
    return item < 10;
})

a; // true
~~~



**some()**

方法是js中的迭代方法，用于检测数组中的**某些元素**是否满足指定条件

* 依次执行数组元素，如果一个元素满足条件就返回true，不会继续执行后面的元素判断；没有满足条件则返回false
* 不会改变原数组

~~~js
var arr = [1, 2, 3, 4, 5, 6];

var a = arr.some(function( item, index, array){
    console.log(item); // 打印 1、2、3、4、5，不会打印6
    return item > 4;
}); 

console.log(a) // true
~~~



### 数组方法（ES6）

| 序号 | 方法        | 描述                                                         |
| ---- | ----------- | ------------------------------------------------------------ |
| 1    | includes()  | 判断数组是否包含该元素，返回Boolean值                        |
| 2    | find()      | 返回符合传入测试（函数）条件的数组元素，**不改变原数组**     |
| 3    | findIndex() | 返回符合传入测试（函数）条件的数组元素索引，**不改变原数组** |
| 4    | for…of 循环 | entries()，keys() 和 values()                                |



**includes()**

判断数组是否包含该元素，返回Boolean值

~~~js
[1, 2, 3].includes(2); // true
[1, 2, 3].includes(4); // false
[1, 2, NaN].includes(NaN); // true
~~~

该方法的第二个参数：

* 表示搜索的起始位置，默认为 0
* 如果第二个参数为负数，则表示倒数的位置，如果这时它大于数组长度（比如第二个参数为 -4，但数组长度为 3 ），则会重置为从 0 开始。

~~~js
[1, 2, 3].includes(3, 3); // false
[1, 2, 3].includes(3, -1); // true
~~~



**find()**

返回符合传入测试（函数）条件的数组元素，**不改变原数组**

~~~js
[1, 2, 3, 4, 5].find(function(item){
   return item > 3;
}) // 4  可以看到只返回一个值
~~~

~~~js
[1, 2, 3, 4, 5].find(function(item, index, arr) {
  return item > 9;
}) // -1  所有元素都不符合条件，则返回-1
~~~

~~~js
var arr = [{ num: 1, name: '111'}, { num: 2, name: '222'}, { num: 3, name: '333'}];
var res = arr.find(i => i.num > 1);
res; // {num: 2, name: "222"}
~~~



 **findIndex()**

返回符合传入测试（函数）条件的数组元素索引，**不改变原数组**

~~~js
[1, 2, 3, 4, 5].findIndex(function(item) {
   return item > 3;
}) // 3  返回索引
~~~

~~~js
[1, 2, 3, 4, 5].findIndex(function(item) {
   return item > 5;
}) // -1 所有元素都不符合条件，则返回-1
~~~

两个方法都可以发现`NaN`，弥补了数组的`indexOf`方法的不足。

```javascript
[NaN].indexOf(NaN); // -1

[NaN].findIndex(i => Object.is(NaN, i)); // 0
```



**用 for…of 循环进行遍历**

`keys()` 是对**键名**的遍历

`values()`是对**值**的遍历

`entries()` 是对**键值对**的遍历

~~~js
for (let index of [1, 2].keys()) {
 console.log(index);
}
// 0
// 1

for (let value of [1, 2].values()) {
 console.log(value);
}
// 1
// 2

for (let [index, value] of [1, 2].entries()) {
 console.log(index, value);
}
// 0 1
// 1 2
~~~



### 数组遍历（for in 和 for of）

**for in 语句用于遍历数组或者对象**

得到的是数组的元素索引，或者是对象的属性key

~~~js
var obj = { a: 10, b: 20, c: 30 };
for(var i in obj) {
    console.log(i +' '+ obj[i]);
}

// a 10
// b 20
// c 30
~~~

~~~js
var arr = [10, 20, 30];
for(var i in arr) {
    console.log(i +' '+ arr[i]);
}

// 0 10
// 1 20
// 2 30
~~~



**for of 语句用于数组遍历，不能遍历对象**

直接得到数组的值

~~~js
var arr = [10, 20, 30];
for(var i of arr) {
    console.log(i);
}

// 10
// 20
// 30
~~~

~~~js
var arr = [{a: 10}, {b: 20}, {c: 30}];
for(var i of arr) {
    console.log(i);
}

// {a: 10}
// {b: 20}
// {c: 30}
~~~



## 函数

### 简介

函数是被设计为执行特定任务的代码块

<img src="https://i.niupic.com/images/2020/02/04/6mSy.jpg" />

<img src="https://i.niupic.com/images/2020/02/04/6mSw.jpg" />

### 函数声明

也称函数定义、函数语句，由`function`关键字组成，包括

* 函数的名称
* 函数括号()，用于传参
* 函数大括号{}

```js
function add(a, b) { // 这里的a，b是形参，且该函数是命名函数 【函数声明】
	return a + b;
}
add(1, 2); // 3 这里的1，2是实参  【函数调用】
```

特点：函数声明的时候，函数体并不会执行，只要当函数被调用的时候才会执行。



### 函数表达式

这样的函数其实是**匿名函数**(没有名称的函数)

存放在变量中的函数不需要函数名。他们总是使用变量名调用

```js
let getSum = function(a, b) { // 这里的a，b是形参，且该函数是匿名函数
	return a + b;
}
getSum(1, 2); // 3
```

当将函数作为**参数**传递给另一个函数时，函数表达式很方便

~~~js
形参：函数在定义的时候小括号里的变量叫形参

实参：函数在调用的时候小括号里传入的值叫实参，实参可以是变量也可以是值

命名函数：函数如果有名字，就是命名函数

匿名函数：函数如果没有名字，就是匿名函数

函数表达式：把一个函数给一个变量，此时形成了函数表达式 ：var 变量 = 匿名函数

回调函数：函数可以作为参数使用，如果一个函数作为参数，那么我们说这个参数(函数)可以叫回调函数
~~~



### 函数调用

定义一个函数并不会自动的执行它

**函数调用**

```js
var getSum = function(a, b) {
	return a + b;
}
getSum(1, 2); // 3
```

**函数表达式自调用**

~~~js
(function() {
	console.log('hello')
})(); // hello
~~~

注意：无法对函数声明进行自调用



### 函数提升

对于函数来说，只有函数声明会被提升到顶部，而函数表达式不会被提升

**函数声明会提升**

~~~js
fn(1, 2); // 3

function fn(a, b) {
	return a + b;
}
~~~

**函数表达式不会提升**

~~~js
fn(1, 2); // error: f is not a function

var fn = function(a, b) {
	return a + b;
}
~~~



### 函数作为值

~~~js
function fn(a, b) {
	return a * b;
}

var x = fn(4, 3) * 2; // 24
~~~



### 函数是对象

~~~js
typeof function fn() {}; // function
~~~

但是最好是把 JavaScript 函数描述为对象



### 函数作用域

在函数内定义的变量不能在函数之外的任何地方访问，因为变量仅仅在该函数的域的内部有定义

~~~js
function fn() {
	var a = 10;
	console.log(a); // 10
}
fn();
console.log(a); // a is not defined
~~~



### 箭头函数（ES6）

#### 箭头函数语法

总结：

箭头函数相当于匿名函数，所以需要变量接收

如果参数只有一个，不需要括号，参数没有或者多个则需要括号

如果代码块部分多于一条语句，需要大括号{}

如果需要返回一个对象，必须在对象外面加上括号



~~~js
var f = () => 'hello'

// 等同于
var f = () => { return 'hello' }

// 等同于
var f = function() { return 'hello' }
~~~

~~~js
// ES5
var f = function(a, b) { return a * b };

// ES6
var f = (a, b) => a * b;
~~~



当箭头函数只有一个参数时，可以省略括号，直接写参数名

~~~js
var f = a => a;
~~~



当箭头函数没有参数或者多个参数是，不能省略括号

~~~js
var f = () => 'hello';
~~~

~~~js
var sum = (a, b) => a + b;
~~~



当箭头函数的代码块部分多于一条语句，就要使用 `{}` 将它们括起来，并且使用 `return` 语句返回

~~~js
var sum = (a, b) => { 
  console.log('hello');
  return a + b; 
}
sum(1, 2);
// hello
// 3
~~~



由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号，否则会报错

```javascript
let getObj = id => ({ id: id, name: 'aaa' });
```



#### 箭头函数示例

箭头函数可以与变量解构结合使用

```javascript
const getName = ({ first, last }) => first + ' ' + last;

// 等同于
function getName(person) {
  return person.first + ' ' + person.last;
}
```



箭头函数使得表达更加简洁。

```javascript
const iseven = n => n % 2 === 0
const square = n => n * n
```



箭头函数的一个用处是简化回调函数。

```javascript
// 正常函数写法
[1, 2, 3].map(function(i) { 
    return i * i;
})

// 箭头函数写法
[1, 2, 3].map(i => i * i);
```

另一个例子是

```javascript
// 正常函数写法
var res = arr.sort(function(a, b) {
  return a - b;
})

// 箭头函数写法
var res = arr.sort((a, b) => a - b);
```



下面是 rest 参数与箭头函数结合的例子

```javascript
const f = (...a) => a;

f(1, 2, 3, 4, 5)
// [1, 2, 3, 4, 5]

const f = (a, ...b) => [a, b];

fn(1, 2, 3, 4, 5)
// [1, [2, 3, 4, 5]]
```



注意: 函数体内的 this 对象，就是定义时所在的对象，而不是使用时所在的对象

`this` 对象的指向是可变的，但是在箭头函数中，它是固定的

~~~js
function foo() {
  setTimeout(() => {
    console.log('id:', this.id);
  }, 100);
}
let id = 21;
foo.call({ id: 42 });
// id: 42
~~~

上面代码中，setTimeout 的参数是一个箭头函数，这个箭头函数的定义生效是在 foo 函数生成时，而它的真正执行要等到 100 毫秒后。如果是普通函数，执行时 this 应该指向全局对象window，这时应该输出 21。但是，箭头函数导致 this 总是指向函数定义生效时所在的对象（本例是{ id: 42}），所以输出的是 42。



#### 箭头函数特性

~~~js
* 没有 this  super  arguments
* 不可以当作构造函数，也就不能通过 new 关键字调用
* 没有原型属性 prototype
* 不可以改变 this 指向
* 不支持重复的命名参数

注意：箭头函数和传统函数一样都有一个 name 属性，这一点是不变的
~~~

**`this指向的固定化，并不是因为箭头函数内部有绑定this的机制，实际原因是箭头函数根本没有自己的this，导致内部的this就是外层代码块的this。正是因为它没有this，所以也就不能用作构造函数`**



**箭头函数没有this，只能从上下文获取this**

箭头函数的`this`值，取决于函数外部非箭头函数的`this`值，如果上一层还是箭头函数，那就继续往上找，如果找不到那么`this`就是`Window`对象

~~~js
var person = {
    f1: () => {
        console.log(this)
    },
    f2: function() {
        return () => { console.log(this) }
    }
}
person.f1();  // Window
person.f2()();  // person对象
~~~



**箭头函数没有arguments对象**

箭头函数也没有`arguments`对象，但是如果它外层还有一层非箭头函数的话，就会去找外层的非箭头函数的`arguments`对象，注意：箭头函数找arguments对象只会找外层非箭头函数的函数，如果外层是一个非箭头函数的函数如果它也没有arguments对象也会中断返回，就不会在往外层去找了，如下

~~~js
var f1 = () => console.log(arguments);  // 执行该函数会抛出错误

function f2(a, b, c) {
    return () => {
        console.log(arguments); // [1, 2, 3]
    }
}
f2(1, 2, 3)();
~~~

可以清楚的看到当前的箭头函数没有`arguments`对象，然而就去它的外层去找非箭头函数的函数。``

~~~js
function fn(a) {
    return function() {
        return () => {
            console.log(arguments); // []
        }
    }
}
fn(1)()();
~~~

上面示例中可以看到，里面的箭头函数往外层找非箭头函数的函数，然后不管外层这个函数有没有`arguments`对象都会返回。只要它是非箭头函数就可以，如果外层是箭头函数还会继续往外层找

~~~js
var f = (...a) => console.log(a);
f(1, 2, 3); // [1, 2, 3]
~~~



**箭头函数不能用`new`关键字声明**

~~~js
var Fn = () => {};
new Fn(); // 抛出错误，找不到constructor对象
~~~



**箭头函数没有原型`prototype`**

箭头函数没有原型，有可能面试官会问，`JavaScript`中所有的函数都有`prototype`属性吗

~~~js
var fn = () => {};
fn.prototype; // undefined
~~~



**箭头函数不能改变`this`指向**

~~~js
var person = {};
var fn = () => console.log(this);

fn.bind(person)(); // Window (不是person)
fn.call(person); // Window (不是person)
fn.apply(person); // Window (不是person)
~~~



#### 箭头函数和普通函数的区别

~~~js
* 相比普通函数, 箭头函数有更简洁的语法
* 箭头函数不绑定 this ，会捕获其所在的上下文的 this 值，作为自己的 this 值
* 箭头函数是匿名函数, 不能作为构造函数，不可以使用 new 命令，否则会抛出一个错误
* 箭头函数没有 arguments，取而代之用 rest参数...解决
* 箭头函数的 this 永远指向其上下文的 this ，任何方法都改变不了其指向，如 call()、bind()、apply() ，可以说正是因为没有自己的 this
* 箭头函数没有原型属性 prototype
~~~





### 回调函数

**回调函数**：一个函数被作为参数传递给另一个函数 

<img src="https://s2.ax1x.com/2020/02/09/1h93mq.png" alt="1h93mq.png" border="0" /> 

**回调函数的基本原理**：使用命名函数或者匿名函数作为回调

 第一种方法：就是匿名函数作为回调（使用了参数位置定义的匿名函数作为回调函数）

第二种方式：就是命名函数作为回调（定义一个命名函数并将函数名作为变量传递给函数 

传递参数给回调函数）

~~~js

~~~

**在执行之前确保回调函数是一个函数**

~~~js
function fn(a, callback){
    // 确保callback是一个函数   
    if(typeof callback === 'function') {
        // 调用它，既然我们已经确定了它是可调用的
        callback(a);
    }
}
~~~





**函数可以作为另一个函数的参数**

```js
var say = function() {
  console.log('hello');
}
function fn(a) {
  a();
}
fn(say); // hello
```

**函数可以作为另一个函数的返回值**

```js
function ex(a) {
  var b = 3;
  return function() {
    console.log(a + b);
  }
}
var fn = ex(2); //此时返回的是一个函数
fn(); // 5
```



### 递归函数

> 调用自身的函数我们称之为递归函数

在某种意义上说，递归近似于循环。两者都重复执行相同的代码，并且两者都需要一个终止条件（避免无限循环或者无限递归

一个函数可以指向并调用自身。有三种方法可以达到这个目的

1. 函数名
2. `arguments.callee`
3. 作用域下的一个指向该函数的变量名

~~~js
function loop(x) {
	if (x >= 10) {
		console.log(x)
		return;
	}
	loop(x + 1); // 递归调用
}
loop(0); // 10
~~~



### 嵌套函数

可以在一个函数里面嵌套另外一个函数。嵌套（内部）函数对其容器（外部）函数是私有的。它自身也形成了一个闭包。一个闭包是一个可以自己拥有独立的环境与变量的表达式（通常是函数）



既然嵌套函数是一个闭包，就意味着一个嵌套函数可以”继承“容器函数的参数和变量。换句话说，内部函数包含外部函数的作用域。

可以总结如下：

- 内部函数只可以在外部函数中访问。
- 内部函数形成了一个闭包：它可以访问外部函数的参数和变量，但是外部函数却不能使用它的参数和变量。

~~~js
function addSquares(a, b) {
  function square(x) {
    return x * x;
  }
  return square(a) + square(b);
}
a = addSquares(2, 3); // 13
~~~

由于内部函数形成了闭包，因此你可以调用外部函数并为外部函数和内部函数指定参数

~~~js
function outside(x) {
  function inside(y) {
    return x + y;
  }
  return inside;
}

a = outside(3)(5); // 8
~~~



### return语句

**`return`语句**终止函数的执行，并返回一个指定的值给函数调用者

~~~js
function add(a, b) {
    return a + b;
}
var sum = add(1, 2);
sum; // 3
~~~

如果省略`retrun`，则返回`undefined`

下面的 return 语句都会终止函数的执行

~~~js
return;
return true;
return false;
return x;
return x + y / 3;
~~~

`自动插入分号（ASI）` 规则会影响 `return` 语句。在 `return` 关键字和被返回的表达式之间不允许使用行终止符。

~~~js
return
a + b;
~~~

根据 ASI，被转换为

~~~js
return;
a + b;
~~~

控制台会警告“unreachable code after return statement”

**主要作用**

**1.中断一个函数的执行**

**2.返回一个函数，关于闭包**

~~~js
function magic(x) {
	return function calc(x) { return x * 10 }
}

var answer = magic();
answer(10); // 100
~~~



### arguments 对象

JavaScript 函数有一个名为 arguments 对象的内置对象

arguments 对象包含函数调用时使用的参数数组

~~~js
function fn(a, b) {
    console.log(arguments);
    console.log(arguments[0]);
}
fn(1, 2);
// Arguments(2) [1, 2, callee: ƒ, Symbol(Symbol.iterator): ƒ]
// 1
~~~





# 重点概念

面向对象：提出需求，找对象，对象解决，注重的是结果

js不是一门面向对象的语言，是基于对象的语言，js来模拟面向对象
面向对象的特性：封装、继承、多态(抽象性)

1、封装：就是包装，把一些重用的内容进行包装，在需要的时候，直接使用
2、继承：类与类之间的关系，js中没有类的概念，js中有构造函数的概念，是可以有继承的，是基于原型
3、多态：同一个行为，针对不同的对象，产生了不同的效果

## 预解析

> 预解析：就是在浏览器解析代码之前，把变量的声明和函数的声明提前(提升)到该作用域的最上面



### 变量的预解析

```js
console.log(a); // undefined
var a = 10;
```

相当于

```js
var a;
console.log(a); // undefined
a = 10;
```

```js
问：什么情况下的结果是 undefined ?
答：
1. 变量声明了，没有赋值，结果是 undefined
2. 函数没有明确返回值，如果接收了，结果也是 undefined
3. 使用不存在的对象属性的返回值是 undefined
4. 通过不存在的数组索引访问数组元素结果是 undefined
```

1、变量声明了，没有赋值，结果是 undefined

```js
var a；
console.log(a)； // undefined
// 和函数声明一样，变量的声明也会在一开始就被放入内存中了，但是并没有赋值，所以在它赋值之前，它的值就是undefined
```

2、函数没有明确返回值，如果接收了，结果也是 undefined

~~~js
function fn() {};
var a = fn();
a; // undefined
~~~

3、使用不存在的对象属性的返回值是 undefined

~~~js
var obj = {
  name: 'hello'
}
obj.age; // undefined
~~~

4、通过不存在的数组索引访问数组元素结果是 undefined

~~~js
var arr = [3, 6, 9];
arr[3]; // undefined
~~~



### 函数的预解析

**命名函数可以预解析**

~~~js
fn(); // hello [说明js肯定是在调用函数之前就将函数放入内存中了]
function fn() {
  console.log('hello');
}
~~~

**匿名函数（函数表达式）不可以预解析**

```js
f();
var f = function() {
  console.log('hello');
}
// Uncaught TypeError: f is not a function
```

**变量和函数重名**

```js
console.log(a); // ƒ a(){console.log('hello')}
var a = 10;
function a() {
  console.log('hello');
}
```

这个就说明了，重名时，函数名优先级高于变量名

```js
将变量和函数的声明提升到当前作用域的最上边(不包括赋值和调用)
当变量和函数名称相同时，优先函数
```



## 作用域和作用域链

### 作用域

> 变量的作用域无非就是两种：**全局变量**和**局部变量**，指变量的使用范围

**全局作用域**

最外层函数定义的变量拥有全局作用域，即对任何内部函数来说，都是可以访问的

```js
var a = 10;
function fn() {
  return a;
}
fn(); // 10
```



**局部作用域**

`函数`中定义的变量是**局部变量**

函数内部的变量只能在函数内部使用，不能在函数外部使用

```js
function fn() {
  var a = 10;
}
fn();
console.log(a); // Uncaught ReferenceError: a is not defined报错
```

注意：函数内部声明变量的时候，一定要使用var命令，如果不用的话，你实际上声明了一个全局变量！

```js
function fn() {
  a = 10;
}
fn();
console.log(a); // 10
```

再来看一个代码：

```js
var a = 10;
function fn() {
  console.log(a); // undefined
  var a = 20;
  console.log(a); // 20
}
fn();
```

相当于，可参考预解析

```js
var a = 10;
function fn() {
  var a; // 提前声明了局部变量
  console.log(a); // undefined
  a = 20;
  console.log(a); // 20
}
fn();
```

只要函数内定义了一个局部变量，函数在解析的时候都会将这个变量`提前声明`



**全局作用域下带var和不带var的区别**

```js
console.log(a); // undefined
var a = 10;
```

```js
console.log(a); // Uncaught ReferenceError: a is not defined
a = 10;
```

a = 10 相当于给window增加了一个a的属性名，属性值是10
var a = 10 相当于给全局作用域增加了一个全局变量a，但是不仅如此，它也相当于给window增加了一个属性名a，属性值是10

**JS中没有块级作用域：一对括号{ }中定义的变量，这个变量可以在大括号外面使用**

```js
while(true) {
  var a = 10;
  break;
}
console.log(a); // 10
```

```js
{
  var a = 100
}
console.log(a); // 100   大括号里面声明的变量外部可以使用
```



### 作用域链

> 作用域链：变量的使用，从里向外，层层的搜索，搜索到了就可以直接使用了

层层搜索，搜索到0级作用域的时候，如果还是没有找到这个变量，结果就是报错

```js
var a = 10;
function f1() {
  var a = 20;
  function f2() {
    var a = 30;
    console.log(a);
  }
  f2();
}
f1(); // 30
```

```js
var a = 10; // 作用域链 级别:0
var b = 20;
function f1() {
  var b = 20;
  function f2() {
    var c = 30;
    console.log(a);
  }
  f2();
}
f1(); // 10
```



## 原型（链）

### 原型

每个对象都会在其内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性时

如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，于是就这样一直找下去，也就是我们平时所说的原型链的概念



**函数的原型prototype**

​	每个函数默认有一个prototype属性（指针），其值指向一个对象，这个对象就是我们所说的原型（原型对象）。原型内有一个constructor属性指向构造函数本身



**实例对象的原型 __ proto __**

​	每个实例对象都有一个内置属性 __ proto __ ，指向创建这个实例的构造函数的prototype原型对象。每一个实例对象都能从该原型中 “继承” 属性和方法。所以构造函数的原型被其创建的每一个实例对象共享，因此也是每个实例对象的原型



~~~js
function Person() {}
var p = new Person();
p.__proto__ === Person.prototype; // true
~~~



1、实例对象的*`__proto__`*和构造函数中的*`prototype`*全等

2、因为实例对象是通过构造函数来创建的，构造函数中有原型对象*`prototype`*

3、实例对象的*`__proto__`*指向了构造函数的原型对象*`prototype`*



**总结三者之间关系：**

1、构造函数可以实例化对象
2、构造函数中有一个属性叫(*`prototype`*)，是构造函数的原型对象
3、构造函数的原型对象(*`prototype`*)中有一个*`constructor`*构造器，这个构造器指向的就是自己所在的原型对象所在的构造函数
4、实例对象的原型对象(*`__proto__`*)指向的是该构造函数的原型对象(*`prototype`*)
5、构造函数的原型对象(*`prototype`*)中的方法是可以被实例对象直接访问的



### 原型链

​	每个对象都有一个原型 __ proto __ ，这个原型对象还可以有他自己的原型 __ proto __ （该原型对象也是由构造函数创建，该构造函数也有prototype属性）。以此类推，形成一个实例与原型的 __ proto __ 链条，即**原型链**

​	查找属性时，先在当前对象找，如果没有则去它的原型对象里找，在没有的话就去原型对象的原型对象里找，这个操作被委托在整个原型链上，链的最终端是null

<img src="https://z3.ax1x.com/2021/05/25/2SYJL8.jpg" width="500px" />



**原型链继承**

可以让子类型构造函数的原型prototype等于父类型构造函数的实例对象，这样，子类型函数的实例对象就添加到了原型链上，可以访问父类型的实例对象及其链.上所有的属性和方法，即实现了继承。

<img src="https://z3.ax1x.com/2021/05/25/2StCm8.jpg" width="500px" />



js通过原型链实现函数或对象的继承

```js
原型的指向可以改变
实例对象的原型__proto__指向的是该对象所在的构造函数的原型对象prototype
构造函数的原型对象(prototype)指向如果改变了，实例对象的原型(__proto__)指向也会发生改变
实例对象和原型对象之间的关系是通过__proto__原型来联系起来的，这个关系就是原型链
最终指向：
实例对象的__proto__------->Person.prototype的__proto__---->Object.prototype的__proto__是null
```



继承是一种关系，类(class)与类之间的关系，JS中没有类，但是可以通过构造函数模拟类，然后通过原型来实现继承
继承也是为了数据共享，js中的继承也是为了**实现数据共享**

```js
// 人类的构造函数
function Person(name, age) {
	this.name = name
	this.age = age
}
// 人类的原型的方法
Person.prototype.say = function() {
	console.log('hello')
}

// 中国人的构造函数，中国人有身份证号
function Chinese(id) {
	this.id = id
}
Chinese.prototype = new Person('李三', 20)
Chinese.prototype.sayChinese = function() {
	console.log('我会说中文')
}

// 美国人的构造函数，美国人没有有身份证号
function American(sex) {
	this.sex = sex
}
American.prototype = new Person('Jack', 18)
American.prototype.sayAmerican = function() {
	console.log('我会说英文')
};
var a = new American('男')
console.log(a.name, a.age, a.sex) // Jack 18 男
a.say() // hello
a.sayAmerican() // 我会说英文
```



###  原型作用

数据共享、节省内存空间，**实现继承**

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.say = function() {
    console.log('hello');
  }
}
p1 = new Person();
p2 = new Person();
p1.say(); // hello
p2.say(); // hello
p1.say == p2.say; // false

for(let i = 0; i < 100; i++) {
  var p = new Person('Jack', 20);
  p.say();
} // 会消耗大量内存
```

通过原型来添加方法，解决数据共享，节省内存空间

```js
function Person(name,age) {
  this.name = name;
  this.age = age;
}

Person.prototype.say = function() {
  console.log('hello');
}

var p1 = new Person();
var p2 = new Person();
p1.__proto__.say(); // hello
p2.__proto__.say(); // hello
console.log(p1.__proto__.say === p2.__proto__.say) // true
console.log(p1.__proto__ == Person.prototype) // true
console.log(p2.__proto__ == Person.prototype) // true
```



## JS循环机制

**Javascript是一门非阻塞单线程脚本语言**



**1.为何单线程？**

一次只能干一件事，比如银行排队

<img src="https://p3.pstatp.com/large/pgc-image/3b70b0c4f4dd43078e7d0ca2e2e111cd" />

**2.为何非阻塞？**

因为单线程意味着任务需要排队，任务按顺序执行，如果一个任务很耗时，下一个任务不得不等待。所以为了避免这种阻塞，我们需要一种非阻塞机制。

如上图， 简单就是，有个人正在办业务，发现忘了拿身份证，不可能一直等她回家拿身份证来，太耗时了。理想情况是她可以回家拿身份证，但这段时间应该办理下一个人的业务



**3.macro task与micro task**

在实际情况中，一直在银行排队的叫同步任务。忘了拿身份证的叫异步任务。异步任务分为两种：**微任务**（micro task)和**宏任务**（macro 

task)

理解方式：忘了拿身份证的有好几个人，有的人离家近，有的人离家远。近的就叫微任务（micro task)，远的就叫宏任务（macro task)

微任务micro task事件：Promises(浏览器实现的原生Promise)、MutationObserver、process.nextTick 

宏任务macro task事件：setTimeout、setInterval、setImmediate、I/O、UI rendering



microtask和macotask执行规则：

<img src="https://p3.pstatp.com/large/pgc-image/88bc0d8c13384eeea76d218d51823e8c" />



## 同步异步

**javascript实现异步的原理**

​		首先js是单线程的语言，即同一时间只能做做一件事。那js如何实现异步的，异步和单线程不是自相矛盾吗？其实，单线程和异步确实不能同时成为一个语言的特性。js选择了成为单线程的语言，所以它本身不可能是异步的，但js的宿主环境（比如浏览器，Node）是多线程的，宿主环境通过某种方式（事件驱动）使得js具备了异步的属性

​		浏览器的内核是多线程的，它们在内核制控下相互配合以保持同步，一个浏览器至少实现三个常驻线程：javascript引擎线程，UI渲染线程，浏览器事件触发线程

### 概念

|      | 描述                                               | 例如               |
| ---- | -------------------------------------------------- | ------------------ |
| 同步 | 发送一个请求，等待返回，然后再发送下一个请求       |                    |
| 异步 | 发送一个请求，不等待返回，随时可以再发送下一个请求 | 网络请求、读取文件 |

### 区别

```js
同步和异步最大的区别就在于：一个需要等待，一个不需要等待。
	广播，就是一个异步例子，发起者不关心接收者的状态，不需要等待接收者的返回信息
	电话，就是一个同步例子，发起者需要等待接收者，接通电话后，通信才开始，需要等待接收者的返回信息
```

### 处理异步的方式

**一、回调函数（callback）**

回调（callback）是指一个函数被作为参数传递到另一个函数里，在那个函数执行完后再执行。（ B函数被作为参数传递到A函数里，在A函数执行完后再执行B ）
假定有两个函数f1和f2，f2等待f1的执行结果，f1()-->f2()；如果f1很耗时，可以改写f1，把f2写成f1的回调函数

~~~js
function f2() {
    console.log('hello')
}
function f1(callback){
　　setTimeout(function () {
　　　　callback()
　　}, 1000);
}
f1(f2)  // 1秒后输出 hello
~~~

​		采用回调的方式，把同步操作变成了异步操作，f1不会堵塞程序运行，相当于先执行程序的主要逻辑，将耗时的操作推迟执行

​		回调函数是异步编程最基本的方法，其优点是简单、容易理解和部署，缺点是不利于代码的阅读和维护，各个部分之间高度耦合，流程会很混乱，而且每个任务只能指定一个回调函数

注意区分 回调函数和异步，回调是实现异步的一种手段，并不一定就是异步，回调也可以是同步

~~~js
function A(callback) {
    console.log('I am A')
    callback()  //调用该函数
}
function B() {
   console.log('I am B')
}
A(B)
// I am A
// I am B
~~~



**二、事件监听**

采用事件驱动模式，任务的执行不取决代码的顺序，而取决于某一个事件是否发生

~~~js
function f1(){
    setTimeout(function(){
       window.alert('123')
    },5000);
}
f1() // 5秒后输出 123
~~~

优点：易理解，可绑定多个事件，每一个事件可指定多个回调函数，可以去耦合，有利于实现模块化
缺点：整个程序都要变成事件驱动型，运行流程会变得不清晰



**三、Promise对象**

Promise 是异步编程的一种解决方案

~~~js
new Promise( function(resolve, reject) {...})
~~~

​		Promise 是一个构造函数，所以可以通过`new Promise()`得到一个实例对象，Promise 实例对象代表一个异步操作

​		每当new一个Promise实例的时候，就会立即执行这个异步操作中代码，也就是说，new的时候，除了能够得到一个promise实例之外，还会立即调用我们为Promise构造函数传递的那个function，执行这个function中的异步操作代码

| **Promise 对象存在以下三种状态** | 描述     |
| -------------------------------- | -------- |
| pending                          | 初始状态 |
| fulfilled                        | 成功状态 |
| rejected                         | 失败状态 |

Promise 对象的初始状态是 pending，最终状态是 fulfilled 或者 rejected，其中 fulfilled 表示成功状态，rejected 表示失败状态。状态只能够由 pending 变成 fulfilled 或 rejected，当 Promise 对象的状态改变后就不可以再改变了

<img src="https://mdn.mozillademos.org/files/8633/promises.png">

既然Promise创建的实例对象，是一个异步操作，那么异步操作的结果，只能有两种状态：

​		状态1：异步执行成功，需要在内部调用成功的回调函数`resolve`把结果返回给调用者

​		状态2：异步操作失败，需要在内部调用失败的回调函数`reject` 把结果返回给调用者

由于Promise的实例是一个异步操作，所以内部拿到的操作结果后，无法return把操作的结果返回给调用者，这时候只能使用回调函数的形式，来把成功或失败的结果，返回给调用者

~~~js
const p = new Promise(function(resolve, reject) {
    setTimeout(function() {
        resolve('hello')
    }, 5000)
})
p.then(function(data) {
    console.log(data)
})
// 5秒后输出 hello
~~~

在Promise构造函数的Prototype属性上，有一个.then方法，也就是只要是Promise构造函数创建的实例对象，都可以访问到.then方法，在new出来的Promise实例下，调用.then方法，预先为这个Promise异步操作，指定成功(resolve)和失败(reject)回调函数



~~~js
function getFileByPath(path) {
    return new Promise(function(resolve, reject) {
        fs.readFile(path, 'utf-8', (error, data) => {
            if(error) return reject(error)
            resolve(data)
        })
    })
}

// .then先执行
getFileByPath('./files/02.txt').then(
function(data) {
    console.log(data)
}, 
funtion(error) {
    console.log(error) 
})
~~~

解决回调地狱

~~~js
getFileByPath('./files/01.txt')
.then(function(data) {
    console.log(data)
    return getFileByPath('./files/02 .txt')
})
.then(function(data2) {
    console.log(data2)
    return getFileByPath('./files/03 .txt')
})
.then(function(data3) {
    console.log(data3)
})
~~~

如果前面的Promise执行失败，我们不想让后续的Promise被终止，可以为每个Promise指定失败回调

~~~js
getFileByPath('./files/01.txt')
.then(function(data) {
    console.log(data)
    return getFileByPath('./files/02 .txt')
}, function(error) {
    console.log(error)
    return getFileByPath('./files/02 .txt')
})
.then(function(data2) {
    console.log(data2)
})
~~~

有时候，我们有这样的需求，如果后续Promise执行，依赖于前面Promise执行的结果，如果前面失败了， 则后面的就没有执行下去的意义了，此时我们想要实现，一旦报错，则立即终止所有Promise的执行

~~~js
getFileByPath('./files/01.txt')
.then(function(data) {
    console.log(data)
    return getFileByPath('./files/02 .txt')
})
.then(function(data2) {
    console.log(data2)
    return getFileByPath('./files/03 .txt')
})
.then(function(data3) {
    console.log(data3)
})
.catch(function(error) {
    console.log(error)
})
// 如果前面有任何的promise执行失败，会立即终止所有promise，并马上进入catch去处理promise中抛出的异常
~~~



~~~js
const someAsyncThing = function(flag) {
	return new Promise(function(resolve, reject) {
		if(flag){
			resolve('ok');
		}else{
			reject('error')
		}
	});
};

someAsyncThing(true).then((data)=> {
	console.log('data:',data); // 输出 'ok'
}).catch((error)=>{
	console.log('error:', error); // 不执行
})

someAsyncThing(false).then((data)=> {
	console.log('data:',data); // 不执行
}).catch((error)=>{
	console.log('error:', error); // 输出 'error'
})
~~~

上面代码中，someAsyncThing 函数成功返回 ‘OK’, 失败返回 ‘error’, 只有失败时才会被 catch 捕捉到。



~~~js
let promise = new Promise(function(resolve, reject) {
  console.log(1);
  resolve();
  console.log(2)
});

promise.then(function() {
  console.log(3);
});

console.log(4);

1 2 4 3
~~~

上面代码中，Promise 新建后立即执行，所以首先输出的是`1`和`2`。然后，`then`方法指定的回调函数，将在当前脚本所有同步任务执行完才会执行，所以`resolved`最后输出

## 正则表达式

### 概念

> 正则表达式：也叫规则表达式，按照一定的规则组成的一个表达式，这个表达式的作用主要是匹配字符串的

原书这么一句话，特别棒：正则表达式是匹配模式，**要么匹配字符，要么匹配位置**，要记住！

​	**正则表达式**是用于匹配字符串中字符组合的模式。在 JavaScript中，正则表达式也是对象。这些模式被用于 [`RegExp`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/RegExp) 的 [`exec`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/exec) 和 [`test`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test) 方法, 以及 [`String`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/String) 的 [`match`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/match)、[`matchAll`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/matchAll)、[`replace`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace)、[`search`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/search) 和 [`split`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/split) 方法。

**元字符**

| 字符 | 说明                                     | 示例                                                         |
| ---- | ---------------------------------------- | ------------------------------------------------------------ |
| .    | 除了\n以外的任意的一个字符               |                                                              |
| []   | 范围                                     | [0-9] 表示：0到9之间的任意的一个数字<br />[a-z] 表示：所有的小写的字母中的任意的一个<br />[0-9a-zA-Z] 表示：所有的数字或者是字母中的一个 |
| \|   | 或者                                     | [0-9]\|[a-z]:  要么是一个数字，要么是一个小写字母            |
| ()   | 分组、提升优先级                         | [0-9] \| ([a-z]) \|  [A-Z]<br />([0-9])([1-5])([a-z]) 三组, 从最左边开始计算 |
| *    | 前面的表达式出现了0次到多次              | [a-z] [0-9]* 小写字母中的任意一个 后面是要么是没有数字的,要么是多个数字的 |
| +    | 前面的表达式出现了1次到多次              | [a-z] [9]+  小写字母一个后面最少一个9,或者多个9              |
| ?    | 前面的表达式出现了0次到1次(阻止贪婪模式) | [4] [a-z]? "1231234i"  i可以没有                             |
| {}   | 限定符 : 限定前面的表达式出现的次数      | {0,} 表示的是前面的表达式出现了0次到多次,和 *一样的<br />{1,} 表示的是前面的表达式出现了1次到多次,和 +一样的<br />{0,1} 表示的是前面的表达式出现了0次到1次,和 ?一样的<br />{5,10} 表示的是前面的表达式出现了5次到10次<br />{4} 前面的表达式出现了4次<br />{  ,10} 错误的，不能这么写 |
| ^    | 以什么开始，或者是取非(取反)             | ^[0-9] 以数字开头<br />^[a-z] 以小写字母开始<br />[ ^ 0-9 ]  取反,非数字<br />[ ^ a-z ]   非小写字母 |
| $    | 以什么结束                               | [0-9] [a-z]$  必须以小写字母结束                             |
| \d   | 数字中的一个                             | [0-9]，表示一位数字                                          |
| \D   | 非数字                                   | [^0-9]，除数字以外的任意字符                                 |
| \s   | 空白符                                   | [\t\v\n\r\f]，包含空格、水平制表、垂直制表、换行、回车、换页符 |
| \S   | 非空白符                                 | [^ \t\v\n\r\f]                                               |
| \w   | 非特殊符号                               | [0-9a-zA-Z_]，表示数字、大小写字母和下划线                   |
| \W   | 特殊符号                                 | [^0-9a-zA-Z_]，表示非单词字符                                |
| \b   | 单词的边界                               |                                                              |

| 字符    | 说明           | 示例 |
| ------- | -------------- | ---- |
| (a)     |                |      |
| (?:a)   |                |      |
| a(?=b)  | 匹配a后面有b   |      |
| a(?!b)  | 匹配a后面没有b |      |
| (?<=b)a | 匹配a前面有b   |      |
| (?!b)a  | 匹配a前面没有b |      |

**?=**、**?!**、**?<=** **? 用于限定它前后的表达式，不能单独使用，本身没有作用

**创建一个正则表达式**

1、使用正则表达式字面量，推荐

~~~js
var reg = /ab+c/;
~~~

2、使用RegExp对象的构造函数

~~~js
var reg = new RegExp("ab+c");
~~~

**正则表达式方法**

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [`exec`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/exec) | 一个在字符串中执行查找匹配的RegExp方法，它返回一个数组（未匹配到则返回 null）。 |
| [`test`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test) | 一个在字符串中测试是否匹配的RegExp方法，它返回 true 或 false。 |
| [`match`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/match) | 一个在字符串中执行查找匹配的String方法，它返回一个数组，在未匹配到时会返回 null。 |
| [`matchAll`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/matchAll) | 一个在字符串中执行查找所有匹配的String方法，它返回一个迭代器（iterator）。 |
| [`search`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/search) | 一个在字符串中测试匹配的String方法，它返回匹配到的位置索引，或者在失败时返回-1。 |
| [`replace`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace) | 一个在字符串中执行查找匹配的String方法，并且使用替换字符串替换掉匹配到的子字符串。 |
| [`split`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/split) | 一个使用正则表达式或者一个固定字符串分隔一个字符串，并将分隔后的子字符串存储到数组中的 `String` 方法。 |

**正则表达式标志**

正则表达式有四个可选参数进行全局和不分大小写搜索。这些参数既可以单独使用也可以一起使用在任何顺序和包含正则表达式的部分中

| 标志 | 描述                                                         |
| :--- | :----------------------------------------------------------- |
| `g`  | 全局搜索。                                                   |
| `i`  | 不区分大小写搜索。                                           |
| `m`  | 多行搜索。                                                   |
| `s`  | 允许 `.` 匹配换行符。                                        |
| `u`  | 使用unicode码的模式进行匹配。                                |
| `y`  | 执行“粘性”搜索,匹配从目标字符串的当前位置开始，可以使用y标志。 |

**示例**

> **exec()**

~~~js
var reg = /d(b+)d/g;
var res = reg.exec("adbbdaaa");
res // ["dbbd", "bb", index: 1, input: "adbbdaaa", groups: undefined]
~~~

> **test()**

~~~js
var reg = /^\d{1,5}$/;
var res = reg.test(12345);
res // true
var res2 = reg.test(12345789);
res2 // false
~~~

> **match()**

<font style="color:red">注意：如果正则表达式不包含 g 标志，str.match()将返回与 RegExp.exec() 相同的结果</font>

使用 match 查找 "Chapter" 紧跟着 1 个或多个数值字符，再紧跟着一个小数点和数值字符 0 次或多次。正则表达式包含 `i` 标志，因此大小写会被忽略

~~~js
var str = 'For more information, see Chapter 3.4.5.1';
var reg = /see (chapter \d+(\.\d)*)/i;
var res = str.match(reg);

console.log(res);

// logs [ 'see Chapter 3.4.5.1',
//        'Chapter 3.4.5.1',
//        '.1',
//        index: 22,
//        input: 'For more information, see Chapter 3.4.5.1' ]

// 'see Chapter 3.4.5.1' 是整个匹配。
// 'Chapter 3.4.5.1' 被'(chapter \d+(\.\d)*)'捕获。
// '.1' 是被'(\.\d)'捕获的最后一个值。
// 'index' 属性(22) 是整个匹配从零开始的索引。
// 'input' 属性是被解析的原始字符串
~~~

**match 使用全局（global）和忽略大小写（ignore case）标志**

match 使用 global 和 ignore case 标志。A-E、a-e 的所有字母将会作为一个数组的元素返回

~~~js
var str = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
var reg = /[A-E]/gi;
var res = str.match(reg);

console.log(res);
// ['A', 'B', 'C', 'D', 'E', 'a', 'b', 'c', 'd', 'e']
~~~

没有使用全局g

~~~js
var str = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
var reg = /[A-E]/i;
var res = str.match(reg);
res
// ["A", index: 0, input: "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz", groups: undefined]
~~~

**一个非正则表达式对象作为参数**

当参数是一个字符串或一个数字，它会使用new RegExp(obj)来隐式转换成一个 [`RegExp`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/RegExp)。如果它是一个有正号的正数，RegExp() 方法将忽略正号

~~~js
var str1 = "NaN means not a number. Infinity contains -Infinity and +Infinity in JavaScript.",
    str2 = "My grandfather is 65 years old and My grandmother is 63 years old.",
    str3 = "The contract was declared null and void.";
str1.match("number");   // "number" 是字符串。返回["number"]
str1.match(NaN);        // NaN的类型是number。返回["NaN"]
str1.match(Infinity);   // Infinity的类型是number。返回["Infinity"]
str1.match(+Infinity);  // 返回["Infinity"]
str1.match(-Infinity);  // 返回["-Infinity"]
str2.match(65);         // 返回["65"]
str2.match(+65);        // 有正号的number。返回["65"]
str3.match(null);       // 返回["null"]
~~~



> **search()**

一个在字符串中测试匹配的String方法，它返回匹配到的位置索引，或者在失败时返回-1

~~~js
var str = 'hello world, how are you?';
var reg = /[^\w\s]/g; // 非数字字母下划线空格
var res = str.search(reg);
res // 11 逗号的索引是11
~~~



> **replace()**

方法返回一个由替换值（replacement）替换一些或所有匹配的模式（pattern）后的新字符串。模式可以是一个字符串或者一个正则表达式，替换值可以是一个字符串或者一个每次匹配都要调用的回调函数

<font style="color:red">原字符串不会改变</font>

~~~js
var str = 'one dog, two dog, three dog';
var reg = /dog/g;
var res = str.replace(reg, 'cat');
res // "one cat, two cat, three cat"
~~~

~~~js
var str = 'one dog, two dog, three dog';
var res = str.replace('dog', 'cat');
res // "one cat, two dog, three dog"
~~~

replace 第二个参数可以是个函数

~~~js
function replacer(match, p1, p2, p3, offset, string) {
  // p1 = 非数字, p2 = 数字,  p3 = 非数字、大小写字母和下划线
  return [p1, p2, p3].join(' - ');
}
var newString = 'abc12345#$*%'.replace(/([^\d]*)(\d*)([^\w]*)/, replacer);
console.log(newString);  // abc - 12345 - #$*%
~~~

在replace()中使用正则表达式

~~~js
var str = 'Hello, One, Two, Three';
var res = str.replace(/two/i, 'One');
res // "Hello, One, One, Three"
~~~

在 replace() 中使用 global 和 ignore 选项

~~~js
var str = 'One Two Three one two three';
var res = str.replace(/one/gi, '123');
res // "123 Two Three 123 two three"
~~~

交换字符串中的两个单词

使用字符串作为参数

| 变量名 | 代表的值                                                     |
| ------ | ------------------------------------------------------------ |
| `$$`   | 插入一个 "$"。                                               |
| `$&`   | 插入匹配的子串。                                             |
| `$` `  | 插入当前匹配的子串左边的内容。                               |
| `$'`   | 插入当前匹配的子串右边的内容。                               |
| `$n`   | 假如第一个参数是 [`RegExp`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/RegExp)对象，并且 n 是个小于100的非负整数，那么插入第 n 个括号匹配的字符串。提示：索引是从1开始 |

~~~js
var str = "John Smith";
var reg = /(\w+)\s(\w+)/;
var res = str.replace(reg, "$2, $1");
console.log(res); // Smith, John
~~~



> **split()**

方法使用指定的分隔符字符串将一个[`String`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/String)对象分割成子字符串数组，以一个指定的分割字串来决定每个拆分的位置

~~~js
var str = 'one two three';
var res = str.split(' '); // ["one", "two", "three"]
res[2] // "three"
~~~

~~~js
var str = 'one two three';
var res = str.split(''); // ["o", "n", "e", " ", "t", "w", "o", " ", "t", "h", "r", "e", "e"]
[2] // "e"
~~~

~~~js
var str = 'one two three';
var res = str.split(); // ["one two three"]
~~~

移出字符串中的空格

~~~js
var names = "Harry Trump ;Fred Barney; Helen Rigby ; Bill Abel ;Chris Hand ";
var reg = /\s*(?:;|$)\s*/;
var nameList = names.split(reg);

nameList // ["Harry Trump", "Fred Barney", "Helen Rigby", "Bill Abel", "Chris Hand", ""]
~~~

限制返回值中分割元素数量

~~~js
var str = "Hello World. How are you doing?";
var res = str.split(" ", 3);

res // ["Hello", "World.", "How"]
~~~

靠正则来分割使结果中包含分隔块

`如果 separator 包含捕获括号（capturing parentheses），则其匹配结果将会包含在返回的数组中`

~~~js
var str = "Hello 1 word. Sentence number 2.";
var res = str.split(/(\d)/);

res // ["Hello ", "1", " word. Sentence number ", "2", "."]
~~~

使用一个数组来作为分隔符

~~~js
lits = myString.split(['|']);

console.log(splits); //["this", "is", "a", "Test"]

const myString = 'ca,bc,a,bca,bca,bc';

const splits = myString.split(['a','b']); 
// myString.split(['a','b']) is same as myString.split(String(['a','b'])) 

console.log(splits);  //["c", "c,", "c", "c", "c"]
~~~



> **正则表达式字符匹配**

**1.两种模糊匹配**

横向模糊匹配：即一个正则可匹配的字符串长度不固定，可以是多种情况

~~~js
let r = /ab{2,5}c/g;
let s = "abc abbc abbbc abbbbbbc";
s.match(r); // ["abbc","abbbc"]
~~~

如 /ab{2,5}c/ 表示匹配： 第一个字符是 "a" ，然后是 2 - 5 个字符 "b" ，最后是字符 "c" ：

横向模糊匹配：即一个正则可匹配某个不确定的字符，可以有多种可能

~~~js
let r = /a[123]b/g;
let s = "a0b a1b a4b";
s.match(r); // ["a1b"]
~~~



**匹配规则**

~~~js
[a-z] // 匹配所有的小写字母 
[A-Z] // 匹配所有的大写字母 
[a-zA-Z] // 匹配所有的字母 
[0-9] // 匹配所有的数字 
[0-9\.\-] // 匹配所有的数字，句号和减号
[\f\r\t\n] // 匹配所有的白字符
~~~

~~~js
^[a-z][0-9]$ // 匹配一个由一个小写字母和一位数字组成的字符串,比如"z2"、"t6"或"g7",但不是"ab2"、"r2d3" 或"b52"
~~~

~~~js
^[^0-9][0-9]$ // 这个模式与"&5"、"g7"及"-2"是匹配的，但与"12"、"66"是不匹配的
~~~

~~~js
[^a-z] //除了小写字母以外的所有字符 
[^\\\/\^] //除了(\)(/)(^)之外的所有字符 
[^\"\'] //除了双引号(")和单引号(')之外的所有字符
~~~

| 字符簇           | 描述                            |
| :--------------- | :------------------------------ |
| ^[a-zA-Z_]$      | 所有的字母和下划线              |
| ^[[:alpha:]]{3}$ | 所有的3个字母的单词             |
| ^a$              | 字母a                           |
| ^a{4}$           | aaaa                            |
| ^a{2,4}$         | aa,aaa或aaaa                    |
| ^a{1,3}$         | a,aa或aaa                       |
| ^a{2,}$          | 包含多于两个a的字符串           |
| ^a{2,}           | 如：aardvark和aaab，但apple不行 |
| a{2,}            | 如：baad和aaa，但Nantucket不行  |
| \t{2}            | 两个制表符                      |
| .{2}             | 所有的两个字符                  |

~~~js
^[a-zA-Z0-9_]{1,}$ //所有包含一个以上的字母、数字或下划线的字符串 
^[0-9]{1,}$ //所有的正数 
^\-{0,1}[0-9]{1,}$ //所有的整数 
^\-{0,1}[0-9]{0,}\.{0,1}[0-9]{0,}$ //所有的小数
~~~

与所有以一个可选的负号(\-{0,1})开头(^)、跟着0个或更多的数字([0-9]{0,})、和一个可选的小数点(\.{0,1})再跟上0个或多个数字([0-9]{0,})，并且没有其他任何东西($)。下面你将知道能够使用的更为简单的方法。

特殊字符"?"与{0,1}是相等的，它们都代表着："0个或1个前面的内容"或"前面的内容是可选的"。所以刚才的例子可以简化为

~~~js
^\-?[0-9]{0,}\.?[0-9]{0,}$
~~~

 特殊字符"*"与{0,}是相等的，它们都代表着"0个或多个前面的内容"。最后，字符"+"与 {1,}是相等的，表示"1个或多个前面的内容"，所以上面的4个例子可以写成 

~~~js
^[a-zA-Z0-9_]+$ //所有包含一个以上的字母、数字或下划线的字符串 
^[0-9]+$ //所有的正数 
^\-?[0-9]+$ //所有的整数 
^\-?[0-9]*\.?[0-9]*$ //所有的小数
~~~



**创建正则表达式对象**

**1.通过构造函数创建对象**

```js
var reg=new RegExp(/\d{5}/);
var str="我的电话是10086";
var flag=reg.test(str);
console.log(flag);//true
```

**2.字面量的方式创建对象**

```js
var reg=/\d{1,5}/;
var flag=reg.test("我的幸运数字:888");
console.log(flag);//true
```

**正则测试**

```js
console.log(/./.test("除了回车换行以为的任意字符"));//true
console.log(/.*/.test("0个到多个"));//true
console.log(/.+/.test("1个到多个"));//true
console.log(/.?/.test("哈哈"));//true
console.log(/[0-9]/.test("9527"));//true
console.log(/[a-z]/.test("what"));//true
console.log(/[A-Z]/.test("Are"));//true
console.log(/[a-zA-Z]/.test("干啥子"));//false
console.log(/[0-9a-zA-Z]/.test("9ebg"));//true
console.log(/b|(ara)/.test("abra"));//true
console.log(/[a-z]{2,3}/.test("arfsf"));//true
```

> 已知 str = '森马男士球鞋+红色+高帮'  gg = '红色+高帮' ，要求去除中间+号：'森马男士球鞋  红色+高帮'

~~~js
a = '森马男士球鞋+红色+高帮';
b = '红色+高帮';
function regStr(a, b) {
    let reg = new RegExp('\\+(' + b.replace(/([+*])/g, '\\$1') + ')$');
    return a.replace(reg, ' ' + b)
}
regStr(a, b)
~~~

<img src="https://i.niupic.com/images/2020/02/04/6mTL.png" />

~~~js
var b = '红色+高帮';
b.replace(/[+*]/g, '\\+'); // "红色\+高帮"
~~~

~~~js
a = '森马男士球鞋+红色+高帮';
b = '红色+高帮';
function regStr(a, b) {
    let reg = new RegExp('\\+(' + b.replace(/([+*])/g, '\\+') + ')$');
    return a.replace(reg, ' ' + b)
}
regStr(a, b)
~~~



### 常见正则表达式

~~~js
// 邮箱
var reg_email_1 = /[0-9a-zA-Z_.-]+[@][0-9a-zA-Z_.-]+([.][a-zA-Z]+){1,2}/;
var reg_email_2 = /^[a-zA-Z0-9_-]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/;

// 身份证：15位或者18位
var reg_idcard_1 = /([1-9][0-9]{14})|([1-9][0-9]{16}[0-9xX])/;
var reg_idcard_2 = /([1-9][0-9]{14})([0-9]{2}[0-9xX])?/;

// QQ号
var reg_qq_1 = /[1-9][0-9]{4,10}/;
var reg_qq_2 = /\d{5,11}/;

// 手机号
var reg_phone_1 = /^1\d{10}/;
~~~



## call()、apply()、bind()的区别

**相同点**

作用：都可以改变this的指向

**不同点**

区别在于接收参数的方式不同



先看明白下面

~~~js
var name = '小王';
var age = 18;
var obj = {
    name: '小张',
    objAge: this.age,
    myFun: function() {
        console.log(this.name + '年龄：' + this.age);
    }
}
obj.objAge; // 18
obj.myFun(); // 小张年龄：undefined
~~~

~~~ js
var a = '哈哈';
function fn() {
    console.log(this.a);
}
fn(); // 哈哈
~~~

比较一下这两者 this 的差别，第一个打印里面的 this 指向 obj，第二个全局声明的 shows() 函数 this 是 window



**1. call()、apply()、bind() 都是用来重定义 this 这个对象的！**

~~~js
var name = '小王';
var age = 18;
var obj = {
    name: '小张',
    objAge: this.age,
    myFun: function() {
        console.log(this.name + '年龄：' + this.age);
    }
}

var person = {
    name: '哈哈',
    age: 20
}

obj.myFun.call(person); // 哈哈年龄： 20
obj.myFun.apply(person); // 哈哈年龄： 20
obj.myFun.bind(person)();  // 哈哈年龄： 20
~~~

以上除了 bind 方法后面多了个 () 外 ，结果返回都一致！



**2. 对比call 、bind 、 apply 传参情况下**

~~~js
var name = '小王';
var age = 18;
var obj = {
    name: '小张',
    objAge: this.age,
    myFun: function(a, b) {
        console.log(this.name + '年龄：' + this.age + ' 来自' + a + '去往' + b);
    }
}

var person = {
    name: '哈哈',
    age: 20
}

obj.myFun.call(person,'成都','上海'); // 哈哈年龄：20 来自成都去往上海
obj.myFun.apply(person,['成都','上海']); // 哈哈年龄：20 来自成都去往上海
obj.myFun.bind(person,'成都','上海')(); // 哈哈年龄：20 来自成都去往上海
obj.myFun.bind(person,['成都','上海'])(); // 哈哈年龄：20 来自成都,上海去往undefined
~~~

从上面四个结果不难看出:

1. 三个函数的第一个参数都是 this 的指向对象
2. call 的参数是直接放进去的，第二第三第 n 个参数全都用逗号分隔（其余参数都直接传递给函数）
3. apply 的所有参数都必须放在一个数组里面传进去
4. bind 除了返回是函数以外，它的参数和 call 一样

**当然，三者的参数不限定是 string 类型，允许是各种类型，包括函数 、 object 等等！**



**bind**

bind()方法主要就是将函数绑定到某个对象，bind()会创建一个函数，函数体内的this对象的值会被绑定到传入bind()中的第一个参数的值，例如：f.bind(obj)，实际上可以理解为obj.f()，这时f函数体内的this自然指向的是obj

~~~js
function f1(x, y) {
  console.log((x + y) + ":=====>" + this.age);
}
var ff=f1.bind(null);
ff(10,20);
//30:=====>undefined
~~~

~~~js
function Person() {
  this.age = 1000;
}
Person.prototype.eat = function () {
  console.log("这个是吃");
};
var per = new Person();

var ff = f1.bind(per, 10, 20);
ff();
//30:=====>1000
~~~

~~~js
function Person(age) {
  this.age=age;
}
Person.prototype.play=function () {
  console.log(this+"====>"+this.age);
};

function Student(age) {
  this.age=age;
}
var per=new Person(10);
var stu=new Student(20);
//复制了一份
var ff=per.play.bind(stu);
ff();
~~~



## this关键字

this是在函数**调用时**创建的执行上下文中自动生成的一个内部属性，它会绑定（指向）一个对象。但是函数在不同的调用方式下其内部this会绑定不同对象



JavaScript 中 this 关键词指的是它所属的对象，它拥有不同的值，具体取决于它的使用位置：

~~~js
在全局环境, this 指向顶层对象 Window
普通函数和普通对象 this 指向顶层对象 Window
在方法中, this 指的是当前所属对象
在构造函数中, this 指向了 new 出来的实例对象
在构造函数中原型定义方法的 this 指向了 new 出来的实例对象
在事件中, this 指的是接收事件的元素
~~~

像 call() 和 apply() 这样的方法可以将 this 引用到任何对象



**全局环境**

普通函数和普通对象this指向顶层对象Window

~~~js
console.log(this);   // Window
~~~



**普通函数和普通对象**

普通函数（无论全局还是局部）直接调用，其this指向全局对象Window

~~~ js
// 全局函数
function fn() {
  console.log(this);
}
fn(); // Window
~~~

~~~js
// 局部函数
function fn() {
  function f() {
    console.log(this);
  }
  f();
}
fn(); // Window
~~~

普通对象

~~~js
const obj = { 
  a: this,  // Window
  b: 10
}
~~~



**对象方法**

当对象的方法被调用时，this指向调用该方法的对象

~~~js
const obj = { 
  a: this,  // Window
  b: function() {
    console.log(this); // obj对象本身  
  }
}
const fn = obj.b;
fn();  // Window
~~~

~~~js
const obj = {
  a: 0,
  b: () => {
    console.log(this);
  }
}
obj.b(); // Window
~~~



**构造函数**

当做构造函数new出来的对象，this指向了即将new出来的实例对象

当做普通函数执行，this指向Window

~~~js
function fn() {
  console.log(this); 
}
fn(); // Window
const obj = new fn();   //  fn{}, 即 obj
~~~



**构造函数prototype属性**

原型定义方法的this指向了实例对象。毕竟是通过对象调用的

~~~js
function Fn() {
  this.a = 10;
  let a = 100;
}
Fn.prototype.fn = function() {
  console.log(this.a);
}
const obj = new Fn();
obj.fn();  // 10 说明指向了obj这个对象
~~~



**特殊情况**

如果在方法里面执行函数，this指向window

~~~js
const obj = {
  a: 0,
  b: function () {
    console.log(this);      // obj
    function c() {
      console.log(this);    // Window
    }
    c();
  }
}
obj.b()   
~~~



**call ,apply, bind**

this指向传入的对象

~~~js
const obj = {
  a: 10
}
function fn() {
  console.log(this)
}
fn.call(obj);      // {a: 10}
fn.apply(obj);     // {a: 10}
fn.bind(obj)();    // {a: 10}
~~~



**箭头函数**

在方法中定义函数应该是指向window，但是箭头函数没有自己的this，所以指向上一层作用域中的this

~~~js
var obj = {
  a: 10,
  b: function () {
    console.log(this); // 指向obj
    c = () => {
      console.log(this); // 指向obj，指向上一层作用域中的this
    }
    c();
  }
}
obj.b();
~~~



## new 操作符

**new 操作符具体干了什么**

```js
function Foo(name) {
  this.name = name;
}
var foo = new Foo('demo')
```

```js
1. 开辟空间，存储创建的新的对象
2. 把this设置为当前的对象
3. 设置属性和方法的值
4. 返回当前的新的对象
```



## 闭包

**概念**

**闭包**是指能够访问其他函数内部变量的函数，简单来说就是函数嵌套函数，内部函数引用外部函数的变量或参数。

闭包的定义即：函数 A 内部有一个函数 B，函数 B 可以访问函数 A 中的变量，那么函数 B 就是闭包。

定义和用法：当一个函数的返回值是另外一个函数，而返回的那个函数如果调用了其父函数内部的其它变量，如果返回的这个函数在外部被执行，就产生了闭包。



**闭包的作用**

1. 访问其他函数内部变量
2. 主要是用来封装变量，即把变量隐藏起来，不让外面拿到和修改，保护变量不被内存回收机制回收（缓存数据）



**闭包的优点和缺点**

​	缓存数据，优点也是缺陷，没有及时的释放

​	由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能

导致内存泄露



**一般如何产生闭包**

- 返回函数
- 函数当做参数传递



**函数模式闭包**：在一个函数中有一个函数

```js
function f1() {
    var a = 10
    function f2() {
        console.log(a)
    }
    f2()
}
f1() // 10
```

```js
function f1(a) {
	return function () {
		console.log(a)
	}
}

var fn2 = f1(10)
fn2() // 10
```

**对象模式闭包**：函数中有一个对象

```js
function fn() {
	var a = 10;
	var obj = {
		num: a
	};
	console.log(obj.num);
}
fn() // 10
```

```js
function fn() {
	var a = 20;
	return {
		num: a
	}
}

var obj= fn()
console.log(obj.num) // 20
```

**闭包小案例**

普通函数

```js
function fn() {
	var a = 10;
	a++;
	console.log(a);
}
fn() // 11
fn() // 11
fn() // 11
```

函数闭包

```js
function fn() {
	var a = 10;
	return function () {
        a++;
        return a;
	}
}
var f = fn();
console.log(f()) // 11
console.log(f()) // 12
console.log(f()) // 13
```

闭包案例产生多个相同的随机数

```js
function fn() {
	var a = parseInt(Math.random()*10+1)
	return function () {
        console.log(a)
	}
}
var ff=fn()
f()
f()
f()
```



```js
function fn() {
    var a = 100
    return function () {
        console.log(a)
    }
}
var f = fn()
var a = 200
f() // 100
```

~~~js
var count = 10; //全局作用域 标记为flag1
function add(){
    var count = 0; //函数全局作用域 标记为flag2
    return function(){
        count += 1; // 函数的内部作用域
        console.log(count);
    }
}
var s = add()
s(); // 1
s(); // 2
~~~

根据作用域链的规则，底层作用域没有声明的变量，会向上一级找，找到就返回，没找到就一直找，直到window的变量，没有就

返回undefined。这里明显count 是函数内部的flag2 的那个count



## 浅拷贝和深拷贝

**什么是浅拷贝？什么是深拷贝？**

**浅拷贝**中原始类型为值传递，对象类型仍为引用传递（一般指的是把对象的第一层拷贝到一个新对象上去）；

**深拷贝**中所有属性都可以进行完全的复制，生成一个与原对象完全不相干的对象，也就是新对象中的所有修改都不会在原对象中有所表现



**浅拷贝实现**

使用**Object.assign()**，该方法可以把任意多个的源对象自身的可枚举属性拷贝给目标对象，然后返回目标对象。但是**Object.assign()** 进行的是浅拷贝，拷贝的是对象的属性的引用，而不是对象本身

~~~js
var a = { count: 1, deep: { count: 2 } };
var b = Object.assign({}, a); // 该方法适用于数组或者对象
// 或者
var b = {...a};

a.count = 2;
b.count; // 1
a.deep.count = 5;
b.deep.count; // 5
~~~

原生 JS 实现

~~~js
function shallowCopy(source) {
    let newSource = {};
    for (item in source) {
        if (source.hasOwnProperty(key)) {
            newSource[key] = source[key];
        }
    }
    return newSource;
}
~~~



**深拷贝实现**

常见的是使用**JSON.parse(JSON.stringify())**实现,方法比较简单方便

~~~js
var a = { count: 1, deep: { count: 2 } };
var b = JSON.parse(JSON.stringify(a));
b.deep.count = 20;
console.log(a); // { count: 1, deep: { count: 2 } } <-- 沒被修改
console.log(b); // { count: 1, deep: { count: 20 } }
console.log(a === b); // false
console.log(a.deep === b.deep); // false
~~~

原生 JS 实现，递归拷贝

递归方法实现深度克隆原理：遍历对象、数组直到里边都是基本数据类型，然后再去复制，就是深度拷贝

~~~js
function deepCopy(source) {
    if (typeof source !== 'object') {
        return '不是对象';
    }
    let isArray = Array.isArray(source);
    let newSource = isArray ? [] : {};
    for (let key in source) {
        if (typeof source[key] !== 'object') {
            newSource[key] = source[key];
        } else {
            newSource[key] = deepClone(source[key])
        }
    }
    return newSource
}
~~~

**默写**

~~~js
function deepCopy(data) {
    if(typeof data !== 'object') return '不是对象';
    let newData = Array.isArray(data) ? [] : {};
    for(let key in data) {
        if(typeof data[key] !== 'object') {
            newData[key] = data[key];
        } else {
            newData[key] = deepCopy(data[key])
        }
    }
    return newData;
}
~~~



**JS内存模型图**

![img](https://i.niupic.com/images/2020/02/04/6mSA.jpg)



* 基本数据类型的特点：直接存储在**栈**(stack)中的数据
* 引用数据类型的特点：存储的是该对象在**栈**中**引用地址**，真实的数据存放在**堆**内存里

~~~js
基本数据类型：number  string  boolean  null  undefined

引用数据类型：object  array  function
~~~



**基本类型是按值访问的，不会影响到其他数据，而引用类型的值是按地址访问的，简单的赋值，实际上只是把地址复制了一遍，修改任意一个值会影响到另外一个**

~~~js
// 基本数据类型，不影响其他变量
var a = 10;
var b = a;
a = 20;
console.log(b); // 10
~~~

~~~js
// 引用数据类型修改，会影响其他变量
var a = { count: 10 };
var b = a
console.log(b.a) // 10
a.count = 20;
console.log(b.count) // 20
~~~

从上面可以看出，基本数据类型，不影响其他变量，所以基本类型的值没有深拷贝的概念。而对象a 赋值给了b，JavaScript引擎只是将a的地址赋值给了b，他们指向同一个内存地址，并没有开辟新的栈，当修改a的值，b也被影响了，这就是浅拷贝

浅拷贝只复制指向某个对象的指针，而不复制对象本身，新旧对象还是共享同一块内存。但深拷贝会另外创造一个一模一样的对象，新对象跟原对象不共享内存，修改新对象不会改到原对象

**简单来说**

* 赋值操作两个变量指向同一个对象，两者互相影响
* 浅拷贝新生成一个对象，对象里面的属性是基本类型，拷贝的就是基本类型的值；如果属性是内存地址（引用类型），拷贝的就是内存地址
* 深拷贝会新生成所有对象（值对象里面层层嵌套对象），对象里面的属性是基本类型，拷贝的就是基本类型的值；如果属性是内存地址（引用类型），会新生成一个对象将内容拷贝进去



## GET和POST的区别

~~~js
1. GET 数据传递是通过 URL 中的 ? 参数  传递到服务端的，可以在地址栏中看到传递的参数，POST 数据是通过请求体传递到服务端的，在界面上看不到

2. GET传递的数据长度有限制，因为 URL 地址长度有限（2048个字符），POST 可以提交任何类型的数据，包括文件，没有长度限制

3. GET 后退不会有影响，POST 后退会重新进行提交

4. GET 请求可以被缓存，POST 不可以被缓存

5. GET 只支持URL编码，POST 支持多种编码方式

6. GET 只支持ASCII字符，POST 没有字符类型限制

7. GET 一般用于数据查询，POST 一般用于表单提交
~~~



## http相关知识点

 <font color="#42B983" size="3">**B/S结构**</font>：浏览器-服务器（Browser/Server）结构

 <font color="#42B983" size="3">**C/S结构 **</font>：客户端-服务器结构

~~~js
                       权限                   路径
        ┌───────────────┴───────────────┐  ┌───┴────┐
  http://username:password@example.com:3000/path/data?key=value&key2=value2#fragid1
  └┬┘   └───────┬───────┘ └────┬────┘   └┬┘           └─────────┬─────────┘ └──┬──┘
  协议        用户信息         主机名     端口                  查询参数          片段
~~~

**HTTP 协议**

 **超文本传输协议**（<font color="#42B983" size="3">**英文**</font>：**HyperText Transfer Protocol**，<font color="#42B983" size="3">**缩写**</font>：<font color="#42B983" size="3">**HTTP**</font>）是互联网上应用最为广泛的一种<font color="#42B983" size="3">**网络协议**</font>

**消息结构**

**General**（大概）

~~~js
Request URL: http://vmiaomalltest.vmiaomall.com/goods?id=eb6a806dcdbb4d96bd32917301125950
Request Method: GET
Status Code: 200 OK
Remote Address: 120.79.28.217:80
Referrer Policy: no-referrer-when-downgrade
~~~

**Response Header**（响应头）

~~~js
Accept-Ranges: none
Connection: keep-alive
Content-Encoding: gzip
Content-Type: text/html; charset=utf-8
Date: Thu, 12 Mar 2020 03:13:58 GMT
ETag: "233be-lFVVifPpeSiCXdB4DZHhDRxugJ0"
Server: openresty/1.13.6.2
Transfer-Encoding: chunked
Vary: Accept-Encoding
~~~

**Request Header**（请求头）

~~~
Accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9

Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
Cache-Control: max-age=0
Connection: keep-alive
Host: vmiaomalltest.vmiaomall.com
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.100 Safari/537.36
~~~

**Query String Parameters**（请求参数）

~~~js
id: eb6a806dcdbb4d96bd32917301125950
~~~



## HTTP状态码

| 状态码 | 描述                                  |
| ------ | ------------------------------------- |
| 200    | 返回正常                              |
| 304    | 服务端资源无变化，可使用缓存资源      |
| 400    | 请求参数不合法                        |
| 401    | 未认证                                |
| 403    | 服务端禁止访问该资源                  |
| 404    | 服务端未找到该资源                    |
| 408    | （请求超时） 服务器等候请求时发生超时 |
| 500    | 服务端异常                            |



## 函数的节流和防抖

**节流**

~~~js
	节流的意思是，规定时间内，只触发一次。比如我们设定500ms，在这个时间内，无论点击按钮多少次，它都只会触发一次。具体场景可以是抢购时候，由于有无数人 快速点击按钮，如果每次点击都发送请求，就会给服务器造成巨大的压力，但是我们进行节流后，就会大大减少请求的次数。
~~~



**防抖**

~~~js
	防抖的意思是，在连续的操作中，无论进行了多长时间，只有某一次的操作后在指定的时间内没有再操作，这一次才被判定有效。具体场景可以搜索框输入关键字过程中实时 请求服务器匹配搜索结果，如果不进行处理，那么就是输入框内容一直变化，导致一直发送请求。如果进行防抖处理，结果就是当我们输入内容完成后，一定时间(比如500ms)没有再 输入内容，这时再触发请求。
~~~



## 0.1 + 0.2 精度丢失问题

0.1和0.2在转换成二进制后会无限循环，由于标准位数的限制后面多余的位数会被截掉，此时就已经出现 了精度的损失，相加后因浮点数小数位的限制而截断的二进制数字在转换为十进制就会变成 0.30000000000000004。

小数的最大数是 17 位，但是浮点的算数并不总是 100% 精准

~~~js
var x = 0.2 + 0.1;         // x 将是 0.30000000000000004
~~~

使用乘除法有助于解决上面的问题

~~~js
var x = (0.2 * 10 + 0.1 * 10) / 10;       // x 将是 0.3
~~~





# 常见JS函数封装

~~~js
// 判断对象时候为数组
function isArray(arr) {
	return Object.prototype.toString.call(arr) === '[object Array]';
}

// 获取数组最大值
function max(arr) {
    return Math.max.apply(null, arr);
}

// 获取数组最小值
function min(arr) {
    return Math.min.apply(null, arr);
}

// 数组求和
function sum(arr) {
    return arr.reduce((pre, cur) => pre + cur);
}

// 数组平均值
function average(arr) {
    let sum = arr.reduce((a, b) => a + b);
    return sum / arr.length;
}

// 数组去重
function uniqueArray(arr) {
    let a = [];
    for(let i = 0; i < arr.length; i++) {
        if(a.indexOf(arr[i]) === -1) {
            a.push(arr[i])
        }
    }
    return a;
}

// 深拷贝
function deepCopy(data) {
    if(typeof data !== 'object') return '不是对象';
    let newData = Array.isArray(data) ? [] : {};
    for(let ket in data) {
        if(typeof data[key] !== 'object') {
            newData[key] = data[key];
        } else {
            newData[key] = deepCopy(data[key]);
        }
    }
    return newData;
}

// 数组排序，数组元素都是数字
function arrSort(arr) {
    return arr.sort((a, b) => a - b);
}

// 数组排序，数组元素都是对象
function arrSort(arr, key) {
    return arr.sort((i, j) => {
        let a = i[key];
        let b = j[key];
        if(a > b) {
            return 1;
        } else if(a < b) {
            return -1;
        } else {
            return 0;
        }
    })
}
~~~





# http.js

~~~js
import axios from 'axios';

const http = axios.create({
	baseUrl: 'http://vmiaomall.com'
})

// 添加请求拦截器
http.interceptors.request.use((config) => {
    showloading(); // 显示加载
    config.url = config.url + '.do'; // 在发送请求之前做些什么
    return config;
  }, function (error) {
    return Promise.reject(error); // 对请求错误做些什么
  });

// 添加响应拦截器
axios.interceptors.response.use((res) => {
    hideLoading(); // 隐藏加载
    if(res.data) {
        return res.data; // 对响应数据做点什么
    }
  }, function (error) {
    return Promise.reject(error); // 对响应错误做点什么
  });

export default http
~~~

或者

~~~js
import axios from 'axios';

axios.defaults.baseURL = 'https://vmiaomall.com/api';

export default {
    get(url, data = {}, options = {}) {
      return new Promise((resolve, reject) => {
        axios.get(url, { params: data }).then(res => {
          if (res.status === 200) {
            resolve(res.data)
          } else {
            Toast(res.data.msg)
          }
        }).
        catch(err = >{
          reject(err) let errMsg = '请求失败！请检查网络';
          if (err.response) errMsg = err.response.data.msg Toast(errMsg)
        })
      })
    },
        
    post(url, data = {}, options = {}) {
      return new Promise((resolve, reject) => {
        axios.post(url, data).then(res => {
          if (res.status === 200) {
            resolve(res.data.msg)
          } else {
            Toast(res.data)
          }
        }).
        catch(err = >{
          reject(err) let errMsg = '请求失败！请检查网络';
          if (err.response) errMsg = err.response.data.msg Toast(errMsg)
        })
      })
    }
  }
~~~





# 面试题

### var, let, const的区别

~~~js
var
var声明变量存在变量提升，可重复声明
全局变量如果页面不关闭，那么var变量就不会释放，就会占空间，消耗内存

let
用来声明变量
不可以重复声明
不存在变量提升
只在声明所在的块级作用域内有效

const
用来声明常量（不可改，只读）
不可以重复声明
不存在变量提升
不可以重新赋值
声明的时候必须初始化（赋值）
只在声明的块级作用域内有效
~~~



### null和undefined的区别

在JavaScript中，`null` 和 `undefined` 几乎相等

~~~js
console.log(typeof undefined);    // "undefined"
console.log(typeof null);       // "object"
console.log(null == undefined);    // true  因为两者都默认转换成了false
console.log(null === undefined);    // false   "==="表示绝对相等，null和undefined类型是不一样的，所出“false”
~~~

**null是一个表示"无"的对象，转为数值时为0；undefined是一个表示"无"的原始值，转为数值时为NaN**

~~~js
Number(null); // 0
5 + null; // 5

Number(undefined); // NaN
5 + undefined; // NaN
~~~



* **`null`表示没有对象，即该处不应该有值**

  ~~~js
  （1） 作为函数的参数，表示该函数的参数不是对象
  （2） 作为对象原型链的终点
  	Object.getPrototypeOf(Object.prototype); // null
  ~~~

  

* **`undefined`表示缺少值，即此处应该有值，但没有定义**

~~~
（1）变量被声明了，但没有赋值时，就等于undefined
（2) 调用函数时，应该提供的参数没有提供，该参数等于undefined
（3）对象没有赋值的属性，该属性的值为undefined
（4）函数没有返回值时，默认返回undefined
~~~

~~~js
var i;
i // undefined

function f(x){console.log(x)}
f() // undefined

var  o = new Object();
o.p // undefined

var x = f();
x // undefined
~~~



### 什么情况下是undefined

```js
1. 变量声明了，没有赋值，结果是undefined
2. 函数没有明确返回值，如果接收了，结果也是undefined
3. 使用不存在的对象属性的返回值是undefined
4. 通过不存在的数组索引访问数组元素结果是undefined
```

~~~js
var a;
console.log(a); // undefined
~~~

~~~js
function fn(a, b) {
	a + b;
}
var f = fn(1, 2);
console.log(f); // undefined
~~~

~~~js
var obj = {
	age: 18
}
console.log(obj.name); // undefined
~~~

~~~js
var arr = [5, 3, 2, 4, 1];
arr[5]; // undefined
~~~





### 几种js跨域的解决方法

- `jsonp`、 `iframe`、`window.name`、`window.postMessage`、服务器上设置代理页面



### 简述cookie，localStorage 和 sessionStorage 

| 存储           | 描述                                                         |
| -------------- | ------------------------------------------------------------ |
| cookie         | 空间小（小于4K），存储容量受限，主要作用是与服务器进行交互   |
| sessionStorage | 空间更大，接口丰富，独立空间，非持久化本地存储，仅仅回话级别存储，这些数据只有在同一个会话中的页面才能访问并且当会话结束后数据也随之销毁 |
| localStorage   | 空间更大，接口丰富，独立空间，持久化本地存储，除非主动删除数据，否则数据永远不会过期 |



### setTimeout和setInterval的区别

~~~js
setTimeout(fn, delay); // 用于延迟执行某一函数，只执行一次

setInterval(fn, delay); // 用于延迟执行某一函数，循环执行，直到取消
~~~



### 请用js编写一个数组去重函数

**最简单数组去重**

~~~js
function uniqueArr(arr) {
	let a = [];
	for(let i = 0; i < arr.length; i++) {
		if(a.indexOf(arr[i] == -1)) {
			a.push(arr[i]);
		}
	}
	return a;
}
~~~



**利用ES6 Set去重（ES6中最常用）**

~~~js
function unique(arr) {
	return Array.from(new Set(arr));
}
~~~

或者

~~~js
function unique(arr) {
	return [...new Set(arr)];
}

var arr = [1, 2, 2, 3, 2];
var a = unique(arr);
console.log(a); // [1, 2, 3]
~~~



### 如何通过JS判断一个数组

**instanceof**

~~~js
var arr = []; 
arr instanceof Array; // true
~~~

**constructor**

`constructor`属性返回对创建此对象的数组函数的引用，就是返回对象相对应的构造函数

~~~js
var arr = []; 
arr.constructor == Array; // true
~~~

**最简单的方法**

~~~js
function isArray(arr) {
	return Object.prototype.toString.call(arr) === '[object Array]';
}
~~~

**ES6新增方法isArray()**

~~~js
var arr = [];
Array.isArray(arr); // true
~~~



### Javascript如何实现继承

~~~js
原型继承、构造继承、实例继承、拷贝继承
~~~



### 前端性能优化

~~~js
减少http请求
添加本地缓存
压缩CSS、JS资源文件
图片懒加载
图片服务器
使用内容发布网络（CDN托管）
~~~



### 为什么要用 Sass/Less

~~~js
这些 CSS 预处理语言可以让 CSS 具有一定的编程风格，在我实际的开发体验中给我带来了许多便捷的地方，并且使用他们更有利于项目的后期维护

1. 可以定义变量
2. 可以嵌套式的书写
3. 提高了样式的复用性
4. 可以定义一些函数
~~~



### HTML5/CSS3 新特性

**HTML5**

~~~html
<header></header>
<footer></footer>
<aside></aside>
<main></main>
<nav></nav>
<section></section>
<article></article>
<canvns></canvas>
<audio></audio>
~~~

~~~js
绘画 canvas
用于媒介回放的 video 和 audio 元素
本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失
sessionStorage 的数据在浏览器关闭后自动删除
语意化更好的内容元素，比如article、footer、header、nav、section
表单控件，calendar、date、time、email、url、search
新的技术webworker, websocket, Geolocation
~~~

~~~js
更多的语义化标签（header/nav/footer/section...）
音频、视频 API
Canvas
webSocket
localStorage/sessionStorage
~~~

**CSS3**

~~~js
新的选择器（属性、伪类、伪元素）
颜色新增 RGBA/HSLA 模式
过渡效果：transition，可实现动画效果
自定义动画
媒体查询
盒子模型
~~~

~~~css
新增各种css选择器
圆角 border-radius
多列布局
阴影和反射
文字特效text-shadow
线性渐变
旋转transform
~~~



### 为什么要有同源限制

同源策略指的是：协议，域名，端口相同，同源策略是一种安全协议

举例说明：比如一个黑客程序，他利用`Iframe`把真正的银行登录页面嵌到他的页面上，当你使用真实的用户名，密码登录时，他的页面就可以通过`Javascript`读取到你的表单中`input`中的内容，这样用户名，密码就轻松到手了



### 谈谈你对ES6的理解

~~~js
新增模板字符串（为JavaScript提供了简单的字符串插值功能）
箭头函数
for-of（用来遍历数据—例如数组中的值。）
arguments 对象可被不定参数和默认参数完美代替。
ES6 将 Promise 对象纳入规范，提供了原生的 Promise 对象。
增加了 let 和 const 命令，用来声明变量。
增加了块级作用域。
let 命令实际上就增加了块级作用域。
还有就是引入 module 模块的概念
~~~



### 请用js去除字符串空格

**方法一：使用replace正则匹配的方法**

~~~js
// 去除所有空格: 
str = str.replace(/\s*/g,'');

// 去除两头空格: 
str = str.replace(/^\s|\s$/g,'');

// 去除左空格：
str = str.replace( /^\s*/, '');

// 去除右空格：
str = str.replace(/(\s*$)/g, '');
~~~

~~~js
var str1 = ' a b c ';
var str2 = str1.replace(/\s*/g, '');
console.log(str2); // abc
~~~

**方法二：使用str.trim()方法**

trim()局限性，无法去除中间的空格

~~~js
var str1 = ' a b c ';
var str2 = str1.trim();
console.log(str2); // a b c
~~~



### 什么是跨域

由于浏览器同源策略，凡是发送请求url的协议、域名、端口三者之间任意一与当前页面地址不同即为**跨域**。存在跨域的情况：

~~~js
1. 网络协议不同，如http协议访问https协议
2. 端口不同，如80端口访问8080端口
3. 域名不同，如 qianduanblog.com 访问 baidu.com
4. 子域名不同，如 abc.qianduanblog.com 访问 def.qianduanblog.com
5. 域名和域名对应ip，如 www.a.com 访问 20.205.28.90
~~~



### 网页从输入网址到渲染完成经历了哪些过程

~~~js
1. 域名解析
2. 发起TCP的3次握手
3. 建立TCP连接后发起http请求
4. 服务器收到请求并响应HTTP请求
5. 浏览器解析htm代码,并请求htm代码中的资源(如js、css图片等)
6. 断开TCP连接（四次挥手）
7. 浏览器对页面进行渲染呈现给用户
~~~



### 堆和栈的区别

~~~js
1. 申请方式的不同，栈由系统自动分配，而堆是人为申请开辟

2. 申请大小的不同，栈获得的空间较小，而堆获得的空间较大

3. 申请效率的不同，栈由系统自动分配，速度较快，而堆一般速度比较慢

4. 存储内容的不同，栈在函数调用时，函数调用语句的下一条可执行语句的地址第一个进栈，然后函数的各个参数进栈，其中静态变量是不入栈的，而堆一般是在头部用一个字节存放堆的大小，堆中的具体内容是人为安排;

5. 底层不同，栈是连续的空间，而堆是不连续的空间
~~~





# 面试题库1

**面试题1**

```js
for(var i=0; i<3; i++) {
    setTimeout(() => {
        console.log(i);
    }, 0)
}
// 打印了3个： 3
```

~~~js
for(var i=0; i<3; i++) {
    setTimeout(() => {
        console.log(i);
    }, 10)
}
// 打印了3个： 3 这道题涉及了异步、作用域、闭包
~~~

~~~js
for(let i=0; i<3; i++) {
    setTimeout(() => {
        console.log(i);
    }, 10)
}
// 0 1 2
~~~



**面试题2**

```js
var a = {};
var b = a;
b.name = "abc";
console.log(a.name); // abc
```



```js
var a = {n: 1};
var b = a;  
a.x = a = {n: 2};
console.log(a); // {n: 2}
console.log(b); // {n: 1, x: {n: 2}}
console.log(a.x);  // undefined
console.log(b.x);  // {n:2}

// b = a 是浅拷贝，所以在堆栈中引用的是一个对象地址
// a===>堆栈中{n:1}
// b=a
// b===>指向a中的{n:1}

而我们这道题 a.x = a = {n: 2}     . 的运算优先级大于赋值运算的优先级
所以先计算     a.x  =  a={n:2}
a和b指向堆栈 {n: 1, x: {n: 2}}
a的输出值：{ n:2 };
b的输出值：{ n:1 , x={n:2} }
```



```js
var a = 1, b = 2, c = 3;
a = b = c;
console.log(a); // 3
console.log(b); // 3
console.log(c); // 3
```



**面试题3**

```js
function fn(...a){
	console.log(a);
}
fn(1, 2, 3) // [1, 2, 3]
```



**面试题4**

```js
var a = null;
console.log(typeof a);// object
```



**面试题5**

```js
var a = 10;
function fn() {
    console.log(a); // undefined
    var a = 20;
    console.log(a); // 20
    
}
fn();
```



**面试题6**

var a='object'; js原生实现对变量a进行克隆

```js
var a = '10086';
var b = a.concat();
console.log(b); // 10086
```

~~~js
var a = 10;
var b = a;
a = 20;
console.log(b); // 10
~~~



**面试题7**

输出以下结果

```js
(function(foo){
	return typeof foo.bar;//"undefined"
})({foo:{bar:1}})
```



**面试题8**

请将下列两个数组按sort重新排序

```js
var arr1=[{index: 0, sort: 2}, {index: 1, sort: 3}, {index: 2, sort: 4}, {index: 3, sort: 1}]

var arr2=[{index: 0}, {index: 1, sort: 2}, {index: 2}, {index: 3, sort: 1}]
```

~~~js
var arr1=[{index: 0, sort: 2}, {index: 1, sort: 3}, {index: 2, sort: 4}, {index: 3, sort: 1}];

var a = arr1.sort((a, b) => a.sort - b.sort );
console.log(a);
// [{index: 3, sort: 1}, {index: 0, sort: 2}, {index: 1, sort: 3}, {index: 2, sort: 4}]
~~~

~~~js
var arr2=[{index: 0}, {index: 1, sort: 2}, {index: 2}, {index: 3, sort: 1}];

var a = arr2.filter(item => item.sort).sort((a, b) => a.sort - b.sort);
console.log(a);
// [{index: 3, sort: 1}, {index: 1, sort: 2}]
~~~





# 面试题库2

**["1", "2", "3"].map(parseInt)答案是多少**

~~~js
['1', '2', '3'].map(parseInt); //  [1, NaN, NaN]
~~~

`[1, NaN, NaN]`因为 `parseInt` 需要两个参数 `(val, radix)`，其中`radix` 表示解析时用的基数

`map`传了 `3`个`(element, index, array)`，对应的 `radix` 不合法导致解析失败



**一个栈的输入顺序是12345，则下列序列中不可能是栈的输出顺序的是（）**

~~~js
A. 23415
B. 54132
C. 23145
D. 15432
答案： B
~~~

解析：栈的出入原则是后进先出，选项B中显示5最先输出，说明其余四个元素已经入栈，其输出序列应为54321

~~~js
A. 12345
B. 54321
C. 43512
D. 45321
答案：C
~~~



**函数aa()运行结果是（D）**

~~~js
var num = 0;
function aa() {
    var num = 1;
    return function() {
        return this.num;
    }()
}
aa(); // 0
A. 报错
B. undefined
C. 1
D. 0
~~~



**以下代码输出结果是（D）**

~~~ js
var f = function g() {
    return 23;
}
typeof g(); // Uncaught ReferenceError: g is not defined
A. number
B. undefined
C. funtion
D. Error
~~~



**下面代码输出结果是什么？为什么？**

~~~js
setTimeout(function() {
    var p = new Promise(function(resolve, reject) {
    	console.log(1);
    	resolve();
	})
    p.then(function() {
        console.log(2);
    })
	console.log(3);
}, 1000)
// 1 3 2
~~~



~~~js
var p = new Promise((resolve, reject) => {
    console.log(5);
    resolve();
}).then(() => {
    setTimeout(function() { console.log(6) }, 0)
    return 7;
}).then(v => {
    console.log(v);
})
console.log(4); // 5 4 7 undefined 6
~~~



**常见的Web攻击手段（AC）**

~~~js
A. 通过xss(cross site script)跨站式脚本攻击
B. 通过域名DNS解析劫持
C. 通过sql注入的方式
D. 通过黑客攻击

// XSS(跨站脚本攻击)
// CSRF（跨站请求伪造）
// SQL注入
// DDOS
~~~



**对 http 相关内容描述正确的是(BCD)**

~~~js
 A. 301 状态码是临时重定向
 B. get ⽅方式只能⽀支持 ASCII 字符
 C. get 在从服务器上获取资源，post 重点在向服务器发送数据
 D. HTTPS 就是 HTTP 加上加密处理
~~~



**设置元素浮动后，该元素的 display 值是多少( A )**

~~~js
A. block	B. 不变 	C. inline	D. inline-block
~~~



**关于JavaScript里的xml处理，以下说明正确的是（BCD）**

~~~js
A. Xml是种可扩展标记语言，格式更规范，是作为未来html的替代
B. Xml一般用于传输和存储数据，是对html的补充，两者的目的不同
C. 在JavaScript里解析和处理xml数据时，因为浏览器的不同，其做法也不同
D. 在IE浏览器里处理xml，首先需要创建ActiveXObject对象
~~~





# 面试题库3

**下面输出结果**

JavaScript的规定，NaN表示的是非数字， 但是这个非数字也是不同的，因此，NaN 不等于 NaN，并且两个NaN永远不可能相等

~~~js
NaN == NaN; // false
NaN === NaN; // false

let num;
console.log(num); // undefined
console.log(num + 10 === NaN); // false

let x = 0.1, y = 0.2
x + y === 0.3; // false
~~~

~~~js
undefined == undefined; // true
undefined === undefined; // true

null == null; // true
null === null; // true
~~~



**正确输出内容是什么**

~~~js
let num = 0;
console.log(num++); // 0
console.log(++num); // 2
console.log(num); // 2
~~~



**下面正确输出结果**

~~~js
parseInt('12'); // 12
parseInt('12a'); // 12
parseInt('b12a'); // NaN

Number('12'); // 12
Number('12a'); // NaN
Number('b12a'); // NaN
~~~



**下面正确输出结果**

~~~js
Boolean(1); // true
Boolean(0); // false
Boolean(-1); // true
Boolean('0'); // true
Boolean(undefined); // false
Boolean(null); // false
Boolean(NaN); // false
Boolean(''); // false
Boolean('hello'); // true

Boolean([]); // true
Boolean({}); // true
~~~



**下面正确输出结果**

~~~js
8 < 7 && 3 < 4; // false
-2 && 6 + 6 && null; // null
1 + 1 && 0 & 5; // 0
~~~



**下面正确输出结果**

~~~js
0 || 23; // 23
0 || false || true; // true
null || 10 < 8 || 10 + 10; // 20
null || 10 < 8 || false; // false
~~~



**下面正确输出结果**

~~~js
-1 ? 'aaa' : 'bbb'; // aaa
'0' ? 'aaa' : 'bbb'; // aaa

var n = '0';
+n ? 'aaa' : 'bbb'; // bbb

Boolean(+'0'); // false
~~~



**下面正确输出结果**

函数同名，以最后定义的为准

~~~ js
f1();
function f1() {
    console.log('aaa');
}
f1();
function f1() {
    console.log('bbb');
}
f1();
// 输出结果是: bbb  bbb  bbb
~~~



**下面正确输出结果**

函数同名，以最后定义的为准

~~~ js
function fn(a, b) {
    console.log('函数1');
}
function fn() {
    console.log('函数2')
}
fn(10, 20);
fn();
// 函数2
// 函数2
~~~



**下面正确输出结果**

~~~ js
var a = function() {
    console.log('aaa');
}
a();

var a = function() {
    console.log('bbb');
}
a();
// aaa
// bbb
注意：匿名函数不会声明提升
~~~



**`上面3题解析`**

~~~js
// 示例1
var a = 1;
console.log(a); // 1
var a = 2;
console.log(a); // 2
~~~

通过两个var声明了两次a变量，结果看起来像是后声明同名变量会覆盖之前的声明，是这样吗？

~~~js
// 示例2
a = 1;
console.log(a); // 1
var a;
console.log(a); // 1
~~~

如果是覆盖，a应该是undefined才对，所以不应是覆盖

~~~js
// 示例3
console.log(a); // undefined
var a = 1;
console.log(a); // 1
~~~

可见，在a声明之前打印a是undefined，我们知道在使用一个变量时必须声明，不然后报错

~~~js
// 示例1
var a;
var a; // 重复声明会被忽视
a = 1;
console.log(a); // 1
a = 2;
console.log(a); // 2
 
 
// 示例2
var a;
a = 1;
console.log(a); // 1
 
 
// 示例3
var a;
console.log(a); //undefined
a = 1;
console.log(a); // 1
~~~

~~~js
// 示例4
fn(10); // 10
 
function fn(a) {
    console.log(a);
}
~~~

由此可见，函数的声明也会有提升的现象，与变量提升一致，也是在编译阶段处理声明



**下面正确输出结果**

~~~js
{
    var a = 2;
    console.log(a);
    let b = 3;
    console.log(b);
}
console.log(a);
console.log(b);
// 2
// 3
// 2
// undefined
~~~



**下面正确输出结果**

~~~js
var a = 60;
var obj = {
    a: 10,
    b: this.a + 10,
    fn: function() {
        return this.a;
    }
 }
obj.a; // 10
obj.b; // 70
obj.fn(); // 10
~~~



**下面正确输出结果**

~~~js
var a = 20;
var obj = {
    a: 10,
    getA: function() {
        return this.a;
    }
}
obj.getA(); // 10
var test = obj.getA;
test(); // 20
~~~



**下面正确输出结果**

~~~js
function Person(name, age) {
    this.name = name;
    this.age = age;
    this.say = function() {
        console.log(this.name + this.age)
    }
}
var a = new Person('aaa', 10);
a.say(); // aaa10

var b = new Person('bbb', 20);
b.say(); // bbb20

b = a;
b.say(); // aaa10

a = b;
a.say(); // aaa10
~~~



**调用对象箭头函数，输出是什么？**

~~~js
var age = 20;
var obj = {
    age: 18,
    say: () => {
        console.log(this.age);
    }
}
obj.say(); // 20
~~~



**下面正确输出结果**

~~~ js
const person = { name: 'aaa' };
function say(age) {
    return `${this.name} is ${age}`;
}
say.call(person, 21); // "aaa is 21"
say.bind(person, 21); // f
~~~



**下面正确输出结果**

~~~js
function Person(name) {
    this.name = name;
    this.say = function() {
        setTimeout(function() {
            console.log(this.name);
            this.name = 'aaa';
        }, 1000)
    }
}
var name = 'Cat';
var p = new Person('Tom');
console.log(this.name);
p.say();
console.log(name,'111');
// Cat
// Cat 111
// Cat 一秒后
~~~

<img src="https://z3.ax1x.com/2021/04/25/czsyKU.png" />



**下面正确输出结果**

~~~js
var arr = [1, 4, 2, 4, 6, 1];
var a = [...new Set(arr)];
a; // [1, 4, 2, 6] 注意顺序
~~~



**下面正确输出结果**

~~~js
setTimeout(() => {
   console.log('setTimeout');
}, 0)

new Promise((resolve, reject) => {
    console.log('promise start');
    resolve('promise ok');
}).then((data) => {
    console.log('then result', data);
})
console.log('success');

// promise start
// success
// then result promise ok
// setTimeout 延迟一段时间
~~~





# 面试题库4

**输出下列代码的console.log的结果顺序**

~~~js
function fn() {
    console.info(1);
    Promise.resolve().then(function() {
        console.log(2);
    })
}
console.log(3);
fn();

setTimeout(function() {
    console.log(4);
}, 0)

var p = new Promise(function(resolve, reject) {
	console.log(5);
	setTimeout(function() {
        console.log(6);
    }, 0)
	resolve();
	console.log(7);
})
p.then(function() {
    console.log(8);
})
console.log(9);
// 我之前答案：3 1 2 5 7 9 8 6 4
// 正确答案： 3 1 5 7 9   2 8 4 6
// 先执行完同步任务
~~~

**`举个例子`**

~~~js
setTimeout(function() {
    console.log(1);
}, 0)
new Promise(function(resolve, reject) {
    console.log(2);
    resolve();
}).then(() => console.log(3))
console.log(4);
// 2 4 3 1

~~~

执行逻辑为：首先解析到定时器，因为是异步任务，所以添加到任务队列中，接下来实例化Promise，立即执行其中的内容，输出2，之后把then中的函数加入任务队列中，执行最后一行代码，输出4。此时任务队列中有两个任务，分别是setTimeout与then。then中的函数属于微任务，JS引擎内部的任务，所以先于setTimeout执行，输出3。最后执行setTimeou，它属于宏任务，浏览器API，输出1。
其实也没有太搞懂这个宏任务和微任务的区别，先记住，等以后学到了再说





**下面代码输出结果**

~~~js
var a = 10;
function fn() {
    console.log(a);
    let a = 20;
}
fn(); // ReferenceError: a is not defined
~~~



**下面代码输出结果**

~~~js
console.log(01 + 0.2 === 0.3); // false
~~~



**下面代码输出结果**

~~~js
console.log(1 + '2' + '2'); // 122
console.log(1 + + '2' + '2'); // 32
console.log(1 + - '1' + '2'); // 02
console.log(+ 1 + '1' + '2'); // 112
console.log('a' -'b' + '2'); // NaN2
console.log('a' -'b' + 2); // NaN
~~~

~~~js
console.log(+ '2'); // 2
console.log(+ + '2'); // 2
~~~



**下面代码输出结果**

~~~js
Array(); // []
Array(3); // [, , ,]  定义了一个长度为3的空数组
Array(1, 2, 3); // [1, 2, 3]
~~~



~~~js
Array.of(); // []
Array.of(3); // [3]
Array.of(1, 2, 3); // [1, 2, 3]
~~~





**下面代码输出结果**

~~~js
function Fn() {
    this.name = '张三';
    var age = 18;
    this.sayAge = function() {
        console.log('my age is ' + this.age);
    }
    this.sayHi = function() {
        console.log('Hi' + name)
    }
}
var p = new Fn();
console.log(p.name); // 张三
console.log(p.age); // undefined
p.sayAge(); // my age is undefined
p.sayHi(); // Hi

// console.log('Hi' + name) 涉及到作用域链，如果当前作用域没有这个name，那么继续往上层作用域找，直至顶层对象this
~~~

解析

~~~js
var name;
console.log(name); // 按照正常思路来说，只是声明了name变量并未赋值，所以按常理来说应该输出 undefined

// 究其原因，是因为window存在一个叫 name 的属性
// 此属性为空，实际上，开发者定义的所有变量，都会成为window的属性，如果变量没有被赋值，则该变量不会覆盖window上的同名属性

console.log(name + 'aaa'); // aaa
console.log(this.name + 'aaa'); // aaa
~~~





**下面代码输出结果**

~~~js
function fn() {
    setTimeout(fn, 0)
}

function fn() {
    return Promise.resolve().then(fn)
}
~~~



**下面代码输出结果**

~~~js
function fn() {
    for(var i = 0; i < 10; i++) {
        if(i === 3) {
            return;
        }
        console.log(i);
    }
}

fn(); // 0 1 2
~~~

~~~js
function fn() {
    [0,1,2,3,4,5,6,7,8,9].forEach(function(i) {
        if(i === 3) {
            return;
        }
        console.log(i);
    })
}
fn(); // 0 1 2 4 5 6 7 8 9  注意没有3

// forEach中不能使用continue和break
// forEach中使用return语句的作用只能跳出当前循环，并不能跳出整个循环

// forEach 循环不能被 return 终止，其作用和 for循环中的 continue 相似 只是跳出当前循环，继续执行下一次循环，在 forEach 中也不能使用 break，continue 来跳出循环 同样会有报错
~~~



**下面代码输出结果**

~~~js
var objA = {a: 10, b: 20};
var objB = objA;
console.log(objA.a); // 10

objB.a = 30;
console.log(objA.a); // 30

setTimeout(function() {
    objA.a = 10;
}, 0) 

console.log(objB.a); // 30
~~~



**下面代码输出结果**

~~~js
var arr = new Set([0,1,2,3,3]);
console.log(arr); // Set(4) {0, 1, 2, 3}
console.log(arr.length); // undefined
~~~





# 面试题库5

**HTML语义化的理解**

* 什么是HTML语义化？

根据内容的结构化（内容语义化），选择合适的标签（代码语义化），能够便于开发者阅读和写出更优雅的代码的同时让浏览器的爬虫和机器更好地解析



* 为什么要语义化?

1. 为了在没有CSS的情况下，页面也能呈现出很好地内容结构、代码结构
2. 用户体验，例如title、alt用于解释名词或解释图片信息的标签尽量填写有含义的词语、label标签的活用
3. 有利于SEO：和搜索引擎建立良好沟通，有助于爬虫抓取更多的有效信息：爬虫依赖于标签来确定上下文和各个关键字的权重
4. 方便其他设备解析（如屏幕阅读器、盲人阅读器、移动设备）以有意义的方式来渲染网页
5. 便于团队开发和维护，语义化更具可读性，遵循W3C标准的团队都遵循这个标准，可以减少差异化



**<!DOCTYPE>作用？ 标准模式和兼容模式各有什么区别？**

```js
声明位于位于HTML文档中的第一行
告知浏览器的解析器用什么文档标准解析这个文档
DOCTYPE不存在或格式不正确会导致文档以兼容模式呈现

标准模式的排版 和JS运作模式都是以该浏览器支持的最高标准运行。
在兼容模式中，页面以宽松的向后兼容的方式显示,模拟老式浏览器的行为以防止站点无法工作。
```



**解释写CSS3的Flex布局，以及适用场景**



**请列举几种隐藏元素的方法**

~~~css
visibility: hidden;

opacity: 0;

display: none;

transform: scale(0);

height: 0; overflow: hidden;
~~~



**为什么script要放到底下**

浏览器在解析到<body>标签之前，不会渲染页面的任何部分。把脚本放到页面顶部会导致明显的延迟，通常表现为显示空白页面，用户无法浏览内容，也无法和页面进行交互。



**重绘重排**

 



**请求类型**

请求类型有8种，我常用的有4种，分别是get、post、put、delete

get主要是用来请求数据的，post主要用来上传数据的，put主要用来修改数据的，delete主要用来删除数据的



# 面试题库6

**以下输出什么**

~~~js
for(var i = 1; i <= 5; i++) {
	setTimeout(() => { console.log(i) }, i * 1000)
}
// 6
~~~



**以下输出什么**

~~~js
function test(x, y, z) {
    console.log(test.length);
    console.log(arguments.length);
    console.log(arguments[2]);
}
test(1, 2);
// 3
// 2
// undefined
~~~



**以下输出什么**

~~~js
(function() {
    var x = y = 1;
}) ();
console.log(x, y); // Uncaught ReferenceError: x is not defined
~~~



**以下输出什么**

~~~js
var a = 101;
var b = a > 100 && (a = 70);
var c = (a > 50) || (a = 25);
console.log(a, b, c); // 70  70  true
~~~



**说说你对浏览器hash的理解**

~~~js
1. hash 路由：
	监听 url 中 hash 的变化，然后渲染不同的内容，这种路由不向服务器发送请求，不需要服务端的支持；
2. history 路由：
	监听 url 中的路径变化，需要客户端和服务端共同的支持；
~~~

知乎：https://zhuanlan.zhihu.com/p/130995492



**以下输出什么**

~~~js
var obj = {
    type: 'Identifier',
    name: 'aaa'
}
var { type, name, value } = obj;
console.log(type, name, value); // Identifier aaa undefined
~~~



**用js算法实现一个函数，函数可以把一个数组拆分成多个数组，并且按每3个一组，如[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]经过此函数变成[[1, 2, 3], [4, 5, 6], [7, 8, 9], [10]]**

~~~js
function group(arr) {
    let a = [];
    for(let i = 0; i < arr.length; i += 3) {
    	a.push(arr.slice(i, i + 3));
	}
    return a;
}
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
group(arr); // [[1, 2, 3], [4, 5, 6], [7, 8, 9], [10]]
~~~



**用JS算法实现把[{name: 'a', class: '一班'}, {name: 'c', class: '三班'}, {name: 'b', class: '二班'}, {name: 'd', class: '一班'}]按班级分组**

~~~js
var arr = [{name: 'a', class: '一班'}, {name: 'c', class: '三班'}, {name: 'b', class: '二班'}, {name: 'd', class: '一班'}];
var a = arr.sort((a, b) => a.class - b.class);
a;
// 0: {name: "a", class: "一班"}
// 1: {name: "c", class: "三班"}
// 2: {name: "b", class: "二班"}
// 3: {name: "d", class: "一班"}
~~~



**vue如何获取路由参数，如何编程式导航**

~~~js
https://www.jianshu.com/p/c6492491d13f?clicktime=1577280094
~~~



**vue如何响应路由参数的变化**

~~~js
https://www.cnblogs.com/restart77/p/13377257.html
~~~



**npm install --save 和 npm install --save-dev的区别**

~~~js
https://blog.csdn.net/pange1991/article/details/88591837
~~~



webpack基础

**什么是bundle，什么是chunk， 什么是modules?**

~~~js
bundle：是由webpack打包出来的文件，

chunk：代码块，一个chunk由多个模块组合而成，用于代码的合并和分割。

module：是开发中的单个模块，在webpack的世界，一切皆模块，一个模块对应一个文件，webpack会从配置的entry中递归开始找出所有依赖的模块
~~~



**webpack构建流程**

~~~js
1. 根据配置，识别入口文件；
2. 逐层识别模块依赖（包括 Commonjs、AMD、或 ES6 的 import 等，都会被识别和分析）；
3. Webpack 主要工作内容就是分析代码，转换代码，编译代码，最后输出代码；
4. 输出最后打包后的代码。
~~~



**说一下loader是何作用**

~~~js
file-loader: 把文件输出到一个文件夹中，在代码中通过相对 URL 去引用输出的文件
url-loader: 和 file-loader 类似，但是能在文件很小的情况下以 base64 的方式把文件内容注入到代码中去
source-map-loader: 加载额外的 Source Map 文件，以方便断点调试
image-loader: 加载并且压缩图片文件
babel-loader: 把 ES6 转换成 ES5
css-loader: 加载 CSS，支持模块化、压缩、文件导入等特性（可以理解为将css代码转换为js代码）
style-loader: 把 CSS 代码注入到 JavaScript 中，通过 DOM 操作去加载 CSS
eslint-loader: 通过 ESLint 检查 JavaScript 代码
less-loader: css预处理
~~~



**webpack打包是如何优化前端性能的**

~~~js
1. 压缩代码。删除多余的代码、注释、简化代码的写法等等方式。可以利用webpack的UglifyJsPlugin和ParallelUglifyPlugin来压缩JS文件， 利用cssnano（css-loader?minimize）来压缩css

2. 利用CDN加速。在构建过程中，将引用的静态资源路径修改为CDN上对应的路径。可以利用webpack对于output参数和各loader的publicPath参数来修改资源路径

3. 删除死代码（Tree Shaking）。将代码中永远不会走到的片段删除掉。可以通过在启动webpack时追加参数--optimize-minimize来实现

4. 提取公共代码。
~~~





# 面试题库7

**事件委托是什么**

~~~js
事件委托是利用事件冒泡，只指定一个事件处理程序来管理某一类型的所有事件。

通俗的讲，事件就是onclick、onmouseover、onmouseout等就是事件，委托呢，就是让别人来做，这个事件本来是加在某些元素上的，然而你却加到别人身上来做，完成这个事件。


为什么要用事件委托？
1. 考虑一个ul，在li的数量非常少的时候，为每一个li添加事件当然会使用for循环；但是数量多的时候这样做太浪费内存，长到上百上千上万的时候，为每个li添加事件就会对页面性能产生很大的影响。
2. 给一个ul里面的几个li添加了事件但是如果动态又生成了li则刚生成的li不具备事件这时就需要用到委托。


作用：
1. 性能要好
2. 针对新创建的元素，直接可以拥有事件


事件委托就是利用事件冒泡原理实现的！
事件冒泡：就是事件从最深节点开始，然后逐步向上传播事件；
例：页面上有一个节点树，div > ul  > li  >  a
比如给最里面的a 加一个click 事件，那么事件就会一层一层的往外执行，执行顺序 a - li - ul - div,  有这样一个机制，当我们给最外层的div添加点击事件，那么里面的ul、li、a做点击事件的时候，都会冒泡到最外层的div上，所以都会触发，这就是事件委托，委托他们父集代为执行事件

使用场景
1. 为DOM中的很多元素绑定相同事件；
2. 为DOM中尚不存在的元素绑定事件；
~~~



**下面代码分别输出什么**

~~~js
var a;
console.log(typeof a); // undefined
console.log(b); // ReferenceError: b is not defined
b = 10;
console.log(typeof b);
~~~



**输出什么**

~~~js
var a = new Object();
var b  = a;
b.name = 'aaa';
console.log(a.name); // aaa
~~~



**http和https的区别**

~~~js
1. HTTP 明文传输，数据都是未加密的，安全性较差，HTTPS（SSL+HTTP） 数据传输过程是加密的，安全性较好。

2. 使用 HTTPS 协议需要到 CA（Certificate Authority，数字证书认证机构） 申请证书，一般免费证书较少，因而需要一定费用。证书颁发机构如：Symantec、Comodo、GoDaddy 和 GlobalSign 等。

3. HTTP 页面响应速度比 HTTPS 快，主要是因为 HTTP 使用 TCP 三次握手建立连接，客户端和服务器需要交换 3 个包，而 HTTPS除了 TCP 的三个包，还要加上 ssl 握手需要的 9 个包，所以一共是 12 个包。

4. http 和 https 使用的是完全不同的连接方式，用的端口也不一样，前者是 80，后者是 443。

5. HTTPS 其实就是建构在 SSL/TLS 之上的 HTTP 协议，所以，要比较 HTTPS 比 HTTP 要更耗费服务器资源。
~~~



**vuex刷新数据丢失怎么解决**

~~~js
1. 将vuex中的数据直接保存到浏览器缓存中（sessionStorage、localStorage、cookie）
2. 在页面刷新的时候再次请求远程数据，使之动态更新vuex数据
3. 在父页面向后台请求远程数据，并且在页面刷新前将vuex的数据先保存至sessionStorage（以防请求数据量过大页面加载时拿不到返回的数据）
~~~



**vue首屏优化**

~~~js
~~~



# 面试题库8

**输出下面运行结果**

~~~js
function Foo() {
  this.goo = function() {
    console.log(1)
  }
}

Foo.prototype.goo = function() {
  console.log(2)
}

Foo.goo = function() {
  console.log(3)
}
              
var p = new Foo();
p.goo(); // 1
~~~



**兼容性布局方式有哪些**

~~~js
~~~



**答案是多少**

~~~js
(function(x) {
    delete x;
    console.log(x);
}) (1 + 5);
//  6
~~~

函数参数无法 delete 删除，delete 只能删除通过 for in 访问的属性，也就是只能删除对象的属性、数组的元素；删除失败也不会报错，所以输出6



**在 JS 中有哪些会被隐式转换为 false**

~~~js
1. undefined
2. null
3. false
4. NaN
5. 0
6. ''
~~~



**事件委托是什么**

~~~js
让利用事件冒泡的原理，让自己的所触发的事件，让他的父元素代替执行
~~~



**那些操作会造成内存泄漏？**

~~~js
1. 闭包
2. 死循环
~~~



**用 js 实现千位分隔符?**

~~~js
function commafy(num) {
  num = num + '';
  var reg = /(-?\d+)(\d{3})/;

  if(reg.test(num)){
    num = num.replace(reg, '$1,$2');
  }

  return num;
}

commafy(1234); // 1,234
~~~



**输出结果**

~~~js
console.log(a); // ƒ a(){}
var a = 3;
function a() {};
console.log(a); //3
~~~



**输出结果**

~~~js
function fn() { 
    return a;
    a = 10;
    function a() {};
}
typeof fn(); // object
// 考点：函数声明提前
~~~



**输出结果**

~~~js
var a = 2;
function fn() { 
    window.a = 3;
    console.log(a);
}
fn(); // 3
~~~



**输出结果**

~~~js
function fn() { 
    a = 10;
}
fn();
console.log(a); // 10
// 如果在函数内没有声明变量，直接给变量赋值，会声明出一个全局的变量
~~~



# 面试题库9

**什么行为会引起重排和重绘**

~~~js
1. 重绘：dom节点的css样式颜色的变化过程叫做重绘 改变的是cssTree 一部分变化，对randerTree影响相对较小。所以相对与重排而言对浏览器性能影响较小

2. 重排：js动态的修改dom 即更改了DOM树了 更改dom树之后 renderTree就变了，renderTree变了也就是要重新建立一个renderTree了 ，这个过程叫做重排
~~~



**http和https的区别**

~~~js
https协议需要到CA申请证书，一般免费证书较少，因而需要一定费用。

http是超文本传输协议，信息是明文传输，https则是具有安全性的ssl/tls加密传输协议。

http和https使用的是完全不同的连接方式，用的端口也不一样，前者是80，后者是443。

http的连接很简单，是无状态的；HTTPS协议是由SSL/TLS+HTTP协议构建的可进行加密传输、身份认证的网络协议，比http协议安全
~~~





**组件化模块化的理解**

~~~js

~~~

