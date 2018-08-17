---
title: LocalStorage和SessionStorage
date: 2018-08-17 22:03:35
tags:
---
## 将前端的变量存储到浏览器本地中
LocalStorage与SessionStorage都是window的api，用于将javascript中的变量进行浏览器本地的存储。常见的使用场景如：弹窗只弹一次。

### 常用的api
``` javascript 
window.localStorage.setItem("a","1");
<!-- 存储的类型都是字符串,储存一个名为”a“,值为”1“的hash -->

window.localStorage.getItem("a")；
<!-- 返回”1“ -->

window.localStorage.clear();
<!-- 清空当前页面地址的所有hash -->

window.localStorage.removeItem("a")
<!-- 移除key为"a"的hash -->
```
sessionStorage相应的api类似。

### 对比

**LocalStorage**

+ LocalStorage 跟 HTTP 无关

+ HTTP 不会带上 LocalStorage 的值

+ 只有相同域名的页面才能互相读取 LocalStorage（没有同源那么严格）

+ 每个域名 localStorage 最大存储量为 5Mb 左右（每个浏览器不一样）

+ 常用场景：记录有没有提示过用户（没有用的信息，不能记录密码）

+ LocalStorage 永久有效，除非用户清理缓存

**SessionStorage**（会话存储）

+ 1、2、3、4 同上

+ SessionStorage 在用户关闭页面（会话结束）后就失效。



