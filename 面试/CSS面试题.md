# CSS面试题

## 介绍一下标准CSS盒模型，与低版本IE的盒模型有什么不同？

盒模型就是元素在网页中的实际占位。有两种：标准盒模型和IE盒模型。  
标准模型是border-box；也就是content+padding+border+margin，宽度是content宽度,设置：box-sizing：content-box  
IE盒模型：宽度是content+padding+border  border-box

### 边距重叠

边界重叠是指两个或多个盒子的相邻边界重合在一起而形成一个单一边界。  
两个或多个块级盒子的垂直相邻边界会重合，他们的边界宽度是相邻边界宽度中的最大值。注意：水平边界不会重合。  
边距重叠的原因是如果块元素的margin-top与它的第一个子元素的magin-top之间如果没有border,padding,inline-content,clearance来分隔，或者块元素的margin-bottom与它最后一个子元素之间没有border,padding,inline-content,height,min-height,max-height分割，那么外边距会塌陷，子元素多余的外边距会被父元素的外边距截断。  
兄弟元素之间的margin取他们之间的最大值。  
空元素的边界重叠：假设有一个空元素，它有外边距，但是没有border或padding，这种情况下，上下外边距就碰到一起了，会发生合并。

### BFC原理

解决边距重叠的一个办法就是创建BFC(块级格式化上下文)。特性如下：

* 处于同一个BFC中的元素相互影响。可能会发生margin折叠。
* BFC在页面上是一个独立的容器，容器里面的子元素不会影响到外面的元素。反之亦然。
* 计算BFC高度时，考虑BFC所包含的所有元素，包括浮动元素也参与计算。
* 浮动盒的区域不会叠加到BFC上。

创建BFC的方法如下：

* 让容器浮动float
* 绝对定位position:absolute, fixed
* 行内块元素 display:inline-block
* 表格单元display:table-cell, table等
* 弹性盒模型display:flex inline-flex
* overflow: 不是visible

### BFC使用场景

防止margin重叠，清除内部浮动，自适应两栏布局

## CSS选择器有哪些? 哪些属性可继承？CSS选择器优先级

选择器：ID选择器，类选择器，标签，相邻选择器，子选择器，后代选择器，通配符*，属性选择器，伪类选择器

继承：  
可继承的样式 font-size,font-family, color,ul,li,dl,dt,dd;  
不可继承的样式：border,padding,margin,width,height

优先级，！important > id > class > tag

## 如何居中div？如何居中一个浮动元素？绝对定位居中?img怎么居中

水平垂直居中DIV：

```css
div {
    position: absolute;
    width: 100px;
    height: 100px;
    margin: auto;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
}
div {
    position: absolute;
    width: 100px;
    height: 100px;
    margin: -50px 0 0 -50px;
    top: 50%;
    left: 50%;
}
```

flex:  

```css
parent {
    display: flex;
    justify-content: center;
    align-items: center;
}
div {
    width: 100px;
    height: 100px;
}
```

未知宽高元素的水平垂直居中：

行内元素：  
使用table布局

```css
#container {
    display: table-cell;
    text-align: center;
    vertical-align: middle
}
#center {}
```

CSS3 transform：

```css
#container {
    position: relative;
}
#center {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: tranlate(-50%, -50%)
}
```

flex也行

## display的值有什么作用

inline 变成行内元素。  
block 显示成块级元素  
none 不显示  
inline-block：行内块元素  
list-item 作为列表显示  
table 显示为块级表格

## position的值有哪些

absolute 绝对定位  
fixed 相对浏览器窗口绝对定位  
relative 相对定位  
static 默认值，无定位  
inherit 继承父级position
sticky 粘性定位，监听scroll事件，在viewport滚动到XX之前为相对定位，之后变成绝对定位固定住。

## CSS3新特性

1. 新增选择器，：not(tag) 选择非此tag的元素 tag:empty 选中没有子集的tag元素
2. 边框的圆角和阴影，boredr-image
3. 背景 background-clip, background-origin, background-size
4. 线性渐变 Linear Gradients
5. 文本阴影 text-shadow,word-wrap, word-break;
6. 2D转换； transform:scale(0.9)|translate(0px, -30px) 3D转换 transform
7. 过渡 transition
8. 动画
9. 盒模型
10. flex布局

## 设计一个满屏的品字形布局

下面的使用float或者inline-block

## 常见兼容性问题

1. 不同浏览器都要同意margin和padding
2. IE6双边距
3. chrome会强制最小字体12px，通过-webkit-text-size-adjust:none来解决

## 设置元素float后，该元素的dispaly是什么

自动变成block

## 什么是CSS预处理器/后处理器

预处理器：LESS,SASS，Stylus，增加css复用性，还有层级，变量等，提高工作效率  
后处理器：PostCSS，用在webpack里，目的通常是给CSS添加私有浏览器属性。实现跨浏览器兼容。

## CSS优化，提高性能的方法

1. 避免过度约束
2. 避免使用后代选择符，链式选择符
3. 使用紧凑的语法
4. 避免不必要的命名空间
5. 避免不必要的重复
6. 使用语义化名称
7. 避免!important
8. 尽量精简规则（POSTCSS会做）
9. 不要滥用字体。
10. 值为0时不加单位

## 浏览器怎么解析CSS选择器

从右向左解析，目的是避免对所有元素进行遍历。

## 元素高度设置百分比是相对于什么的百分比

设定padding-top,padding-bottom,等时，百分比是相对于父容器的宽度

## em/rem/px的区别

PX 像素单位
em： 相对父节点字体大小，如父元素的font-size是16px那1em = 16px
rem: 相对于HTML根元素的大小

## 实现三栏水平的圣杯布局

```css
.container {
    padding: 0 300px 0 200px;
}
.left,.main,.right {
    position: relative;
    min-height: 130px;
    float: left;
}
.left {
    left: -200px;
    margin-left: -100%;
    width: 200px;
}
.right {
    right: -300px;
    margin-left: -300px;
    wdith: 300px
}
.main {
    wdith: 100%
}
```

## 移动端媒体查询

文件加载时：

```html
<link rel="stylesheet" type="text/css" href="xxx.css" media="only screen and (max-device-width:480px)">
```

CSS: @media only screen and (max-device-width:480px) 

## 完美分割三栏布局

1.使用table

```css
.container {
    display: table;
}
.child {
    display: table-cell;
}
```

2. flex

```css
.container {
    display: flex;
}
.child {
    flex: 1
}
```
