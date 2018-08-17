---
title: session与cookie
date: 2018-08-17 21:38:11
tags:
---

## session
简单来说，session是基于Cookie实现的。Cookie是服务器发送到浏览器上的一小段文本，这个文本是明文的，浏览器跟用户是可以看到并进行修改的。

如果需要传递一些敏感信息的话，并不安全，所以有了session这样的应用。

## session的实现

1. 在服务器端开辟一段内存，存储一个hash表。

2. hash表类似于{11221.1213123:{email:23882@qq.com;password:123456}},每一个随机数，对应一个用户的相关信息。

3. 当向浏览器返回cooki时，带上对应用户的随机数（sessionID）

4. 当浏览器再次向服务器访问时，带上的cookie包含一个sessionID，服务器只用去响应的内存中，查找相应的hash表。

### 总结

**Cookie**

服务器通过 Set-Cookie 头给客户端一串字符串

客户端每次访问相同域名的网页时，必须带上这段字符串

客户端要在一段时间内保存这个Cookie

Cookie 默认在用户关闭页面后就失效，后台代码可以任意设置 Cookie 的过期时间

大小大概在 4kb 以内

**Session**

将 SessionID（随机数）通过 Cookie 发给客户端

客户端访问服务器时，服务器读取 SessionID

服务器有一块内存（哈希表）保存了所有 session

通过 SessionID 我们可以得到对应用户的隐私信息，如 id、email
这块内存（哈希表）就是服务器上的所有 session

