---
title: Flex实战
date: 2018-08-02 21:36:54
tags:
---

# 前言

之前写过Flex布局的相关属性介绍，但是都是文字表面，在实际运用中的flex布局的思路并没有。在一次面试中，遇到了实际问题，然后今天记录一下flex布局的思路。

## 如何用上flex
**flex的重要概念：** container 和 items <br>
把所有需要布局的东西放在一个容器里面（可以想象成一块桌布container上摆着一些东西items）。
``` html
      <div class="parent" >
        <div class="child">1111111<br>1111111<br>
        1111111<br>1111111</div>
        <div class="child" >2222<br>2222<br>2222</div>
        <div class="child">33<br>33</div>
        <div class="child">44</div>
        <div class="child">55</div>
        <div class="child">66</div>
      </div>
```
这里的parent块就是包含若干个child块的一个container。<br>
接下来就是这些个child如何布局的问题了。<br>
**默认：** 桌布（container）的宽度默认情况是视图宽度，如果有样式width：100px，那么就是100px宽了～

## 关于container的布局
``` css
    .parent{
        display:flex; 
        /* 在container上说明要使用flex布局 */
        flex-direction: row;
        /* 默认主轴方向就是行 */
        flex-wrap: wrap; 
        /* 默认情况是nowrap不换行的，当桌布 */
        /* 不够大时（项目的宽度之和大于容器的宽度），不换行的情况下， */
        /* 会压缩各个项目的宽度 */
        /* flex-flow是flex-direction以及flex-wrap的简写 */
        justify-content: center; 
        /* 在主轴方向上，让桌布上的物品都居中摆放 */
        align-items:center;
        /* 在侧轴方向上，物品居中摆放 */
        /* 这边说明一下items的高度问题，在桌布上摆放的物品， */
        /* 他们的对齐方式都是基于各个物品的高度，而这个高度不等 */
        /* 同于他们的内容，例如height：100px */
        align-content:space-between;
        /* 用于多列或者多行情况的摆放方式 */
    }
```
一般情况，桌布大小需要包含所有的物品，这样container的这些属性，只是用于控制物品之间的空隙，不会去改变物品自身的大小。

``` css
*{margin:0px;padding:0px}

.parent{
  display:flex;
  border:1px solid red;
  align-items: center;
  justify-content:center;
}
.child{
  border:1px solid green;
}

.child:nth-child(2){
  height:200px;
}

```
![](/images/flexContainer.png)

## 关于items的布局

``` css
    .child{
        flex-grow:1;
        /* 如果桌布比较大，空出来很多空间， */
        /* 物品自身的大小可以通过flex-grow得到相应比例的多余空间 */
        flex-shrink:1;
        /* 桌布不够时，物品收缩的比例 */
        flex-basis:100px;
        /* 不论物品多大，都只给桌布上100px的大小 */
        /* flex是上面三个的简写 */
        order: 1;
        /* 用于改变当前项目的顺序 */
        align-self:center;
        /* 等同于container的align-content的效果，不过只用于当前项自身 */
    }
```
关于items的属性，除了order是改变显示的顺序，align-self改变对齐方式外，其余属性是为了分配多余的桌布空间，从而改变自身的大小。

``` css
*{margin:0px;padding:0px}

.parent{
  display:flex;
  border:1px solid red;
  align-items: center;
  justify-content:center;
}
.child{
  border:1px solid green;
}

.child:nth-child(2){
  height:200px;
  order:1;
}

.child:nth-child(1){
  order:2;
  flex-grow:1;
}
.child:nth-child(3){
  align-self: flex-start;

```
![](/images/flexItems.png)