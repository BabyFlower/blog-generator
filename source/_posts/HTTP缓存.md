---
title: HTTP缓存
date: 2018-08-17 22:36:41
tags:
---

## Cache-Control
针对一些服务器返回的js，css，图片等资源时，为了避免浏览器每次发送请求，都要进行下载，在http响应头中添加Cache-Control，告诉浏览器在一定时间内，如果是相同的url请求，就不要再发了。

``` http
HTTP/1.1 200 OK
Content-Type: application/javascript; charset=utf-8;
Cache-Control: max-age = 30; 
<!-- 30内不要再向这个url发送请求了，请直接用浏览器的缓存 -->
var a;.....
```

**注意：** 首页不能设置Cache-Control，如果设置了，那么用户访问的首页将会从浏览器缓存中的网页，不能及时的得到最新的网页信息。

## 实现更新
一般情况下，对于js，css文件Cache-Control会设置一年的时间，如果这个期间部分文件更新了，怎么实现更新呢？

``` html
 <link rel="stylesheet" href="https://www.example.com/main.js">

 <!-- 如果请求相同的url，由于设置了Cache-Control，浏览器会不再发送请求了，所以用下面的方式来变化url -->

 <link rel="stylesheet" href="https://www.example.com/main.js？v=1">
 <!-- 后面加上了参数，这样就会重新发起请求 -->

 <link rel="stylesheet" href="https://www.example.com/main.2112414.js">
 <!-- 可以改变中间的随机数来重新发起请求 -->
```

## Expires 
``` http
Expires：Thu，15 Apr  2010  20：00：00  GMT;  
```
通过指定一个具体的时间，在这个时间点内，不要再发送请求了，直接用缓存。

**如果已经设置了Cache-Control,则expires会被忽略。**

由于expires是基于本地时间的，当本地的时间出现错乱时，就不靠谱了，所以后面才出现了Cache-Control。

## ETag
通过MD5摘要算法将文件进行计算，得到一个md5值，存放在ETag字段中。

``` http
Etag="fca75d26f6dc8111a7d1b24e9debd652"
```
服务器将文件对应的MD5值，通过Etag发给浏览器，当浏览器刷新或者重新向服务器请求相同的url时，会自动在http请求头加上if-none-match：对应的MD5
值，如果服务器发现这个值跟自己文件MD5值是一致的，说明文件没有更新和变化，就不会再发送文件，而是返回304状态值（未修改）。

Etag与Cache-Control的区别是，ETag每次都会发送请求，但是Cache-Control是请求都不会发的。
