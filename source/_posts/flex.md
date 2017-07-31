---
title: "flex布局"
date: 2017-02-06 14:27:40
tags:
categories: 'html-css'
comments: true
---

# flex布局

以前也看过一些flex的文章，感觉好记性不如烂笔头，所以才有了这篇文章。文章主要对flex各个知识点做详细介绍，如果有错误和遗漏，望指点。
<!--more-->

概念
============================
Flex是Flexible Box的缩写，意为"弹性布局"，也称弹性盒子布局。目前高版本浏览器基本都支持flex布局
![](http://okyal4bzs.bkt.clouddn.com/flex-15.jpg)

1、弹性容器(Flex container)
　　任何一个标签都可以指定为flex布局
　　包含着弹性项目的父元素。通过设置 display 属性的值为 flex 或 inline-flex 来定义弹性容器。
```css
/*块级元素*/
.box{
    display: -webkit-flex; /* Safari */
    display: flex;
}
/*行内元素*/
.box{
    display: -webkit-inline-flex; /* Safari */
    display: inline-flex;
}
```
***注意，设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。***

2、弹性项目(Flex item)
　　弹性容器的每个子元素都称为弹性项目,简称为项目。弹性容器直接包含的文本将被包覆成匿名弹性单元。

3、轴(Axis)
　　每个弹性框布局包含两个轴。项目沿其依次排列的那根轴称为主轴(main axis)。垂直于主轴的那根轴称为侧轴(cross axis)。

 4、方向(Direction)
　　弹性容器的主轴起点(main start)/主轴终点(main end)和侧轴起点(cross start)/侧轴终点(cross end)描述了弹性项目排布的起点与终点

5、行(Line)
　　根据 flex-wrap 属性，弹性项目可以排布在单个行或者多个行中。此属性控制侧轴的方向和新行排列的方向

6、尺寸(Dimension)
　　根据弹性容器的主轴与侧轴，弹性项目的宽和高中，对应主轴的称为主轴尺寸(main size) ，对应侧轴的称为 侧轴尺寸(cross size)。

![](http://okyal4bzs.bkt.clouddn.com/flexbox.png)

弹性盒子属性
=================

### 容器上的属性
1、flex-direction：定义主轴的方向
```css
.flex_box {
  flex-direction: row | row-reverse | column | column-reverse;
}
/*
　　row为默认值，代表主轴为水平轴，方向为从左到右。
　　row-reverse代表主轴为水平轴，方向为从右到左。
　　column代表主轴为垂直轴，方向为从上到下。
　　column-reverse代表主轴为垂直轴，方向为从下到上。
*/
```
2、flex-wrap：flex-wrap定义flex项目是否换行显示。默认情况下，flex项目会尽可能地显示在一行当中，即默认值为nowarp
```css
.flex_box {
    flex-wrap: nowrap | wrap | wrap-reverse;
}
/*
    nowrap为默认值，代表不换行。
    wrap代表换行，但默认为第一行在上方。
    wrap-reverse代表换行，但默认为第一行在下方。
*/
```
3、flex-flow：flex-direction和flex-wrap的合并写法，它同时定义了主轴方向与容器内项目的换行方式，其默认值为row nowarp
```css
.flex_box {
    flex-flow: <‘flex-direction’> || <‘flex-wrap’>;
}
```
4、justify-content：定义了项目在主轴上的对齐方式。
*注意：justify-content只会在主轴项目仍具有剩余空间时才会起作用。*
```css
.flex_box {
    justify-content: flex-start | flex-end | center | space-between | space-around;
}
/*
    flex-start为默认值，代表项目在主轴上向起始方向对齐。
    flex-end代表项目在主轴上向结束方向对齐。
    center代表项目在主轴上居中对齐。
    space-between代表项目在主轴上两端对齐，但第一个项目在主轴的起始位置，最后一个项目在主轴的结束位置。
    space-around代表项目在主轴上等分间距，但第一个项目与最后一个项目距离主轴的两端保持一定的距离，这个距离为项目之间间距的1/2。
*/
```
5、align-items：定义了项目在交叉轴上的对齐方式。
```css
.flex_box {
    align-items: flex-start | flex-end | center | baseline | stretch;
}
/*
    flex-start代表项目在交叉轴上向起始方向对齐。
    flex-end代表项目在交叉轴上向结束方向对齐。
    center代表项目在交叉轴上居中对齐。
    baseline代表项目在交叉轴上向项目的第一行文字的基线对齐。
    stretch代表项目在交叉轴上拉伸对齐。
*/
```
6、align-content：定义多根主轴线的对齐方式。当我们把容器的flex-warp的值设置为warp或者warp-reverse时，若项目不能在一根主轴上显示，容器便会出现多根主轴。
```css
.flex_box {
    align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
/*
    flex-start代表多条平行的主轴在交叉轴的起始位置对齐。
    flex-end代表多条平行的主轴在交叉轴的结束位置对齐。
    center代表多条平行的主轴在交叉轴上居中对齐。
    space-between代表多条平行的主轴在交叉轴上两端对齐，但第一条主轴在交叉轴的起始位置，最后一条主轴在交叉轴的结束位置。
    space-around代表多条平行的主轴在交叉轴上等分间距，但第一条主轴与最后一条主轴距离主轴的两端保持一定的距离，这个距离为其它主轴之间间距的1/2。
    stretch为默认值，代表多条平行的主轴拉伸对齐。
*/
```

### 项目上的属性
1、order：定义项目在主轴上的排列顺序。数值越小，排列越靠前，默认值为0。
```css
.flex_item {
    order: <integer>;
}
```

2、flex-grow：定义了项目的放大比例。如果所有伸缩项目的flex-grow设置了1，那么每个伸缩项目将设置为一个大小相等的剩余空间。如果你给其中一个伸缩项目设置了flex-grow值为2，那么这个伸缩项目所占的剩余空间是其他伸缩项目所占剩余空间的两倍
*注意：负值对该属性无效。*
```css
.flex_item {
    flex-grow: <number>; /* default 0 */
}
```
3、flex-shrink：与flex-grow用法类似，不过作用缺相反,flex-shrink定义了项目的缩小比例。其默认值为1。如果所有项目的flex-shrink都为1，当空间不足时，都将等比例缩小。如果所有项目都为1，但其中一个项目的flex-shrink为0，即代表空间不足时，该项目缩小0倍，即为不缩小。
*注意：负值对该属性不起作用。*
```css
.flex_item {
    flex-shrink: <number>; /* default 0 */
}
```
4、flex-basis：定义了在分配多余空间之前，项目占据的主轴空间。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
```css
.flex_item {
    flex-basis: <length> | auto; /* default auto */
}
```
4、flex：flex是flex-grow、flex-shrink和flex-basis的简写，默认值为0 1 auto。后两个属性可选。
```css
.flex_item {
    flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```
5、align-self：定义了单个项目上在交叉轴的对齐方式。 其默认值为继承容器的align-items属性。
```css
.flex_item {
    align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

参考文档：[<font color=#0099ff size=3>flex基础语法介绍</font>](http://www.xingbofeng.com/css-grid-flex/flex/baseflex.html)
　　　　　[<font color=#0099ff size=3>Flex 布局教程：语法篇</font>](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
　　　　　[<font color=#0099ff size=3>flexbox-CSS3弹性盒模型flexbox完整版教程</font>](http://caibaojian.com/flexbox-guide.html)
