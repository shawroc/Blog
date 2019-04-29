# CSS 常见样式

## 块级元素 行内元素

- 块级(block-level); 行内(内联、inline-block-level);
- 块级可以包含块级和行内，行内只能包含文本和行内
- 块级占据一整行空间，行内占据自身宽度空间
- 宽高设置、内外边距的差异

block-level

``` md
div h1 h2 h3 h4 h5 h6 p hr
form ul dl ol pre table
li dd dt tr td th
```

inline-level

``` md
em strong span a br img
button input label select textarea
code script
```

宽高

只对块级元素设置生效，对行内元素设置无效

``` html
<style>
  .box {
    width: 200px;
    height: 100px;
    background-color: red;
  }
</style>
<div class="box"></div>
```

边框

border-width, border-color, border-style

``` css
.box {
  border-width: 1px;
  border-color: red;
  border-style: solid; /* dotted dash */
}

/* 简写 */
.box2  {
  border: 1px dotted #ccc;
}
```

使用边框做三角形

``` css
.t0 {
  height: 20px;
  width: 20px;
  border-top: 20px solid red;
  border-left: 20px solid green;
  border-right: 20px solid orange;
  border-bottom: 20px solid blue;
}
```

``` css
.t1 {
  height: 0;
  width: 0;
  border-top: 20px solid red;
  border-bottom: 20px solid blue;
  border-left: 20px solid transparent;
  border-right: 20px solid transparent;
}
```

paddinng 

- padding 代表内边距，有四个方向的值，可以合写，值可以是数值也可以是百分比（相对于父容器、不是自身）
  - padding-top
  - padding-right
  - padding-bottom
  - padding-left

``` css
padding: 20px; /* padding: 20px 20px 20px 20px */
padding: 10px 20px; /* padding: 10px 20px 10px 20px */
padding: 10px 20px 30px; /* padding: 10px 20px 30px 20px */
```

margin

- margin 代表外边距，有四个方向的值，可以合写，值可以是数值也可以是百分比（相对于父容器、不是自身）。还可以是负值
- 外边距合并问题

margin-top, margin-right, margin-bottom, margin-left

``` css
margin: 20px; /* margin: 20px 20px 20px 20px; */
margin: 10px 20px; /* margin: 10px 20px 10px 20px; */
margin: 10px 20px 30px; /* margin: 10px 20px 30px 20px; */
```

margin: 0 auto;

对于块级元素 设置 margin: 0 auto 可达到居中目的

``` css
.box {
  /* margin: 0 auto; 实际上是下面两个起作用 */
  margin-left: auto;
  margin-right: auto;
}
```

去除元素的默认样式

``` css
* {
  margin: 0;
  padding: 0;
}
```

display

- 块级： block, list-item, table
- 行内： inline, inline-table, inline-block

display
value: inline | block | list-item | inline-block | table | table-row-group | table-row | table-cell | 

Initial: inline
Applies to: all elements
Inherited: no

font 

- font-size: 字体大小
- font-family: 字体；宋体、微软雅黑、Arial 等
- font-weight: 文字粗度，常用的就是默认值 regular 和 粗体 bold
- line-height: 行高，可以用百分比、倍数或者固定尺寸
- 以上属性都可继承给子元素

用法

``` css
body {
  font: 12px/1.5 tahoma,arial,'Hiragino Sans GB','\5b8b\4f53',sans-serif;
}

p {
  line-height: 1.5;
  font-size: 14px;
  font-family: 'Helvetica Neue',Helvetica,Arial,sans-serif;
  font-weight: bold;
}

```

font-family

使用浏览器打开页面时，浏览器会读取 HTML 文件进行解析渲染。
当读到文字时会转换成对应的 unicode 码（可以认为是世界上任意一种文字的特定编号）。 再根据 HTML 里设置的 font-family （如果没设置则使用浏览器默认设置）去查找电脑里（如果有自定义字体 @font-face，则加载对应字体文件）对应的字体文件。找到文件后根据 unicode 码去查找绘制外形，找到后绘制到页面上。

font-family 的写法

在 CSS 中设置字体时，直接写字体中文或英文名称浏览器都能识别，直接写中文的情况下编码（GB2312、UTF-8 等）不匹配时会产生乱码。保险的方式是将字体名称用 Unicode 来表示。

宋体 | SimSun | \5B8B\4F53 黑体 | SimHei | \9ED1\4F53 微软雅黑 | Microsoft YaHei | \5FAE\8F6F\96C5\9ED1

打开控制台 escape('微软雅黑'), 把 %u 替换成 \

Chrome 最小字体
chrome 默认字体大小 16px，最小字体 12px

文本

- text-align: 文本对齐方式 left、center、right、justify
- text-indent: 文本第一行缩进距离
- text-decoration: none、underline、line-through、overline
- color:  文字颜色
- text-transform: 改变文字大小写 none、uppercase、lowercase、capitalize
- word-spacing: 可以改变字（单词）之间的标准间隔
- letter-spacing: 字母间隔修改的是字符或字母之间的间隔

单行文本溢出加...

``` css
.card > h3 {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

颜色

- 单词：red, blue, pink, yellow, white, black
- 十六进制: #000000, #fff, #eee, #ccc, #666, #333, #f00, #0f0,#00f
- rgb: rgb(255, 255, 255), rgb(0, 255,0)
- rgba: rgba(0,0,0,0.5)
- 更多

单位

- px: 固定单位
- 百分比（宽高？文字大小？line-height? position?）
- em: 相对单位，相对于父元素字体大小
- rem: 相对单位，相对于根元素（html）字体大小
- vw vh: 相对单位，1 vw 为屏幕宽度的 1% 兼容性


a 链接设置颜色

a 有默认颜色和样式，会覆盖继承的样式

``` css
a {
  color: red;
  text-decoration: none;
}
```

列表去掉点

``` css
ul {
  list-style: none;
}

li {
  list-style: none;
}
```

隐藏 or 透明

- opacity: 0; 透明度为 0，整体
- visibility: hidden; 和 opacity: 0 类似
- display: none; 消失，不占用位置
- background-color: rgba(0,0,0,0.2) 只是背景色透明
