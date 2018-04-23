---
title: BFC简介
date: 2018-04-20 15:28:21
tags:
---
## BFC(block formatting context,块格式化上下文)
*针对div，1.它没有定义，2.它只有特性/功能*

### 功能1:爸爸管儿子(不叫清除浮动)
>     display:inline block inline-block(非块盒的块容器)
浮动，绝对定位元素，非块盒的块容器，overflow不为visible
>     display:table-cell/table-caption display:flow-root,则该元素为BFC
不管内容如何，BFC总会包住儿子，也可用border边框实现。
>     display:flow-root 让当前元素触发BFC

### 功能2
在竖直方向上，同一BFC中，两个块级元素的margin会合并(取最大)

### 功能3:爸爸管儿子，儿子管孙子，则爸爸不管儿子
在一个BFC中的内容，被另一个BFC包括，则不管该该部分内容

### 功能4:BFC包住内容，可不发生重叠
让两个相邻的元素，界限分明 
