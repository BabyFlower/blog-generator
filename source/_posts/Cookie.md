---
title: Cookie
date: 2018-08-17 20:25:05
tags:
---

## cookie在哪？
+ cookie是服务器保存在浏览器上的一小段文本信息。

+ 服务器端响应前端请求时，在http响应头设置cookie。

``` http
    HTTP/1.0 200 OK
    Content-type: text/html
    Set-Cookie: yummy_cookie=choco
    Set-Cookie: tasty_cookie=strawberry
    <!-- 可以设置多个cookie -->
```

+ 当浏览器接收到http响应之后，会将该cookie以及对应的域名A进行存储。

+ 当浏览器再次访问与域名A同源的地址时，http请求会自动附上这段cookie。

``` http
    GET /sample_page.html HTTP/1.1
    Host: www.example.org
    Cookie: yummy_cookie=choco; tasty_cookie=strawberry
    <!-- 请求带多个cookie，用；进行分割 -->
```

### cookie在什么时候会带上

    当用户浏览www.baidu.com时，服务器响应头设置了cookie，那么浏览器将会记录域名www.baidu.com以及根路径“/”，当浏览器访问www.baidu.com/question等所有子路径时，都会带上cookie。

    而当用户浏览www.baidu.com/picture时，服务器在响应头中设置了Cookie，那么只有浏览器访问www.baidu.com/picture及其子路径时才有效。


### cookie的一些特点

+  不同的浏览器，不同的cookie

+ cookie存储在本地的磁盘中

+ 浏览器可以对cookie进行修改

+ cookie有有效期的，默认20分钟左右，浏览器会自动进行清理

+ 响应头的Set-Cookie可以对cookie进行时长进行限定。

+ 不同浏览器对 Cookie 数量和大小的限制，是不一样的。一般来说，单个域名设置的 Cookie 不应超过30个，每个 Cookie 的大小不能超过4KB。

### 响应头中Set-Cookie的一些常见设置

1. 指定cookie对应的域名与路径

``` http
 Set-Cookie: key1=value1; domain=example.com; path=/blog
 <!-- 如果要修改上面cookie中key1的值，那么对应的domain跟path都要一致 -->

 Set-Cookie: key1=value2; domain=example.com; path=/
 <!-- 由于这里的path不同，那么浏览器会重新存储一个新的cookie -->
 <!-- 当浏览器再次访问example.com/blog时，请求中Cookie:key1=value2; key1=value1 -->
```
2. 指定浏览器保存cookie的时间Expires，Max-Age

``` http
Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT;
<!-- Expires属性指定一个具体的到期时间，到了指定时间以后，浏览器就不再保留这个 Cookie。它的值是 UTC 格式，可以使用Date.prototype.toUTCString()进行格式转换。 -->

Set-Cookie: id=a3fWa; Max-Age=3600;
<!-- Max-Age属性指定从现在开始 Cookie 存在的秒数，比如60 * 60 * 24 * 365（即一年）。过了这个时间以后，浏览器就不再保留这个 Cookie。 -->
```
3. HttpOnly

``` http
Set-Cookie:id=237@qq.com ; HttpOnly;

<!-- HttpOnly属性指定该 Cookie 无法通过 JavaScript 脚本拿到，主要是Document.cookie属性、XMLHttpRequest对象和 Request API 都拿不到该属性。这样就防止了该 Cookie 被脚本读到，只有浏览器发出 HTTP 请求时，才会带上该 Cookie。但是通过浏览器还是可以对cookie进行修改。 -->
```



