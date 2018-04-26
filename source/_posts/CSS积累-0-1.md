---
title: CSS积累_0.1
date: 2018-04-23 13:46:16
tags:
---
## CSS简介
Cascading Style Sheets (CSS) is a stylesheet language used to describe the presentation of a document written in HTML or XML (including XML dialects such as SVG or XHTML). CSS describes how elements should be rendered on screen, on paper, in speech, or on other media. 

### 导入CSS
+ style 标签
+ style 属性
+ @import url(./a.css)

### 横向排列
``` css
float:left;  /*子元素添加float属性*/
.clearfix::after{
    content:"";
    display:block;
    clear:both;
}  /*父元素添加clearfix类，用于清除浮动*/
```
**清除浮动:** 当父级元素内的子元素浮动时，可能会导致父级元素的高度塌陷，即父级元素包不住子元素。清除浮动使父元素的高度始终由子元素的高度决定，避免塌陷现象。

### 去除原有样式
``` css
text-decoration:none;/*去除下划线*/
list-style:none;/*去除li标签的点样式*/
```

### li>a 高度不一致
>     li>a{display:block}

![默认](https://github.com/BabyFlower/blog-generator/blob/master/source/_posts/liaWoutDisBlock.png)
![display:block](https://github.com/BabyFlower/blog-generator/blob/master/source/_posts/liaWithDisBlock.png)



