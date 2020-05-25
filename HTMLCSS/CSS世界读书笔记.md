# 第1章 概述

​		CSS 世界的诞生就是为图文信息展示服务的。

## 1.1 何为“流”

**CSS 世界中的“流”指的是什么呢？**

​		“流”实际上是 CSS 世界中的一种基本的定位和布局机制，可以理解为现实世界的一套物理规则，“流”跟现实世界的“水流”有异曲同工的表现。

<img src="C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200518091931443.png" alt="image-20200518091931443" style="zoom:67%;" />

​	所谓“流”，就是 CSS 世界中 <u>**引导元素排列和定位**</u> 的一条看不见的“水流”。





# 第2章 需提前了解的术语和概念

## 2.1 选择器

![image-20200518093206449](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200518093206449.png)



## 2.2 关系选择器

![image-20200518093601171](C:\Users\hang_\AppData\Roaming\Typora\typora-user-images\image-20200518093601171.png)





# 第3章 流、元素与基本尺寸

​		把 HTML 常见标签分为两类：块级元素（block-level element）和内联元素（inline element）

## 3.1 块级元素

​		常见的块级元素有 div、li、table

​		**“块级元素”和“display 为 block 的元素”不是一个概念**。例如，<li>元素默认的 display 值是 list-item，<table>元素默认的 display 值是 table，但是它们均是“块级元素”，因为它们都符合块级元素的基本特征，也就是**一个水平流上只能单独显示一个元素，多个块级元素则换行显示**。

​		使用“块级元素”具有换行特性，可以配合 clear 属性来清除浮动带来的影响。例如：

```html
<div class="box clear">
    <img src="/images/common/l/1.jpg">
</div>
<style>
.box {
    padding: 10px;s
    background-color: #cd0000;
}
.box > img {
    float: left;
}
***************************************************************
.clear:after {
    content: "";
    display: table;  // 也可以是 block，或者是 list-item
    clear: both;
}
</style>
http://demo.cssworld.cn/3/1-1.php
```



















































































