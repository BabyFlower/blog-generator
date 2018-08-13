---
title: 同源策略CORS
date: 2018-08-13 15:26:26
tags:
---

## 同源策略
浏览器的同源策略：

浏览器只有在协议+端口+域名一模一样才允许发送AJAX，读取Cookie，LocalStorage，IndexDB以及获得DOM。

[阮一峰的浏览器同源政策及其规避方法](http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html)

## CORS(Cross-origin resource sharing)
这篇博客主要针对于ajax的只能同源使用的限制，利用CORS跨域资源请求，来进行不同源的ajax请求。

``` http
http://www.example.com/dir/page.html
http://www.example.com/dir2/other.html：同源
http://example.com/dir/other.html：不同源（域名不同）
http://v2.www.example.com/dir/other.html：不同源（域名不同）
http://www.example.com:81/dir/other.html：不同源（端口不同）
```
### 流程情况（简单请求）

当一个网源A向不同源的网源B发起ajax请求时：

+ 浏览器会自动在请求头中，加入Origin字段，信息为网源A的地址（协议+域名+端口）

+ 当服务器接收到请求之后，获取Origin字段信息，检查是否在许可范围内

+ 若满足许可，则响应头中，加入如下字段

``` http
    Access-Control-Allow-Origin: http://api.bob.com（！必须）
    Access-Control-Allow-Credentials: true  （可选）
    Access-Control-Expose-Headers: FooBar   （可选）
```
+ 浏览器接收到请求之后，自动解析响应头中的Access-Control-信息，若包含A网源，则自动完成ajax请求

+ 若浏览器没有接收到Access-Control-信息或者不包含A网源，则抛出异常，可被XMLHttpRequest的onerror回调函数捕获（！！注意，这种错误无法通过状态码识别，因为HTTP回应的状态码有可能是200。）

当在实际情况中，ajax的CORS实现主要是在服务器端，响应头需要添加包含Access-Control-信息的字段。

上述的流程只是针对简单的CORS请求，非简单请求请参考 [阮一峰的跨域资源共享 CORS 详解](http://www.ruanyifeng.com/blog/2016/04/cors.html)

### JSONP对比
简单来说： JSONP只支持GET, 而CORS支持所有类型的请求。

