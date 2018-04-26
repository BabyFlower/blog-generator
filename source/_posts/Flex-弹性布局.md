---
title: Flex-弹性布局
date: 2018-04-26 22:35:59
tags:
---

**1. flex布局与方向无关**
**2. 空间自动分配，自动对齐**
**3. 适用于简单的线性布局，更复杂的布局交给grid布局**

![](https://github.com/BabyFlower/blog-generator/blob/master/source/_posts/flexbox.png)

## flex container(弹性容器) 
*包含弹性项目的父元素，通过设置display 属性的值为 flex 或 inline-flex 来定义弹性容器*

### 属性
+ **flex-direction:** 确定主轴，row从左到右(默认)，row-reverse从右到左，column从上到下，column-reverse从下到上
+ **flex-wrap:** 换行/列，nowrap(默认)，wrap
+ **flex-flow:** 上面两个的简写
+ **justify-content:** 主轴对齐方式，space-between，space-around,flex-start(往起点靠),flex-end(终点)，center
+ **align-items:** 测轴对齐方式，stretch(伸展为最高元素一样)，flex-start，flex-end,center
+ **align-content:** 多行/列内容对齐方式，baseline(文字对齐)，stretch(默认，平均分布)，space-between,space-around,flex-start,flex-end

## flex-item
*弹性容器的每个子元素都称为弹性项目。弹性容器直接包含的文本将被包覆成匿名弹性单元*

### 属性
+ **flex-grow:** 增长比例，分配多余空间(默认为0，不放大)
+ **flex-shrink:** 收缩比例，默认为1，设置为0时，不参与收缩
+ **flex-basis:** 默认大小auto，默认的宽度由内容决定
+ **flex:** 上面三个的缩写，auto(1 1 auto),none(0 0 auto)
+ **order:** 排列顺序
+ **align-self:** 自身对齐方式(高度不能写死)，flex-end，center，flex-start
