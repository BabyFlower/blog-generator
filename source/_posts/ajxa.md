---
title: ajxa
date: 2018-08-10 15:17:22
tags:
---

## 谁能发送请求
1. 用 form 可以发请求，但是会刷新页面或新开页面<br>
``` javascript
  <form action="/xxx" method="post">
   <input type="password" name="password">
    <input type="submit">
  </form>
```
2. 用 a 可以发 get 请求，但是也会刷新页面或新开页面<br>
``` javascript
 <a href="/xxx">lala</a>
```
3. 用 img 可以发 get 请求，但是只能以图片的形式展示<br>
``` javascript
  <img src="/xxx" alt="图片">
```
4. 用 link 可以发 get 请求，但是只能以 CSS、favicon 的形式展示<br>
``` javascript
    let link = document.createElement("link");
    link.rel = "stylesheet";
    link.href = '/xxx';
    document.body.appendChild(link); //执行这句时，才会发起请求
```
5. 用 script 可以发 get 请求，但是只能以脚本的形式运行<br>
这就是早期的跨域策略思想--jsonp，需要后端返回js执行回调函数。
``` javascript
  let script = document.createElement('script')
  let functionName = 'frank'+parseInt(Math.randow()*100000,10)
  window[functionName] =  function(result){
    if(result==='success'){
      alert('success')
      }else{
        alert('fail')
      }
  }        //添加全局的回调函数
  script.src = 'http://127.0.0.1:8080/pay?callback='+functionName;
  document.body.appendChild(script);
  script.onload = function(e){
    e.currentTarget.remove(); //当script加载成功时，把标签移除
    delete window[functionName] //移除全局的回调函数
  }
  script.onerror = function(e){
    e.currentTarget.remove(); //当script加载失败时，把标签移除
    delete window[functionName] //移除全局的回调函数      
  }
```

## ajax的出现

**解决的问题:**

+ get、post、put、delete,可选择的请求类型

+ 只接受数据，不附带刷新页面或者新开页面的限制

**演变的过程：**
+  IE 5 在JS中引入对象ActiveX, 令JS可以直接发起HTTP请求

+ 其他浏览器引入XMLHttpRequest，并被纳入 W3C 规范

+ Jesse James Garrett 基于XMLHttpRequest发明ajax

## ajax简介

AJAX (Async Javascript and XML，异步的js和xml)，简单来说，一开始的设计是：

1. 使用 XMLHttpRequest 发请求

2. 服务器返回 XML 格式的字符串

3. JS 解析 XML，并更新局部页面

后面随着json的诞生，普遍使用json格式传输数据，从而代替了XML格式。

## XMLHttpRequest实现简单的ajax

### 给出node.js写的简单server后端
``` javascript
#!/usr/bin/env node
var http = require('http')
var fs = require('fs')
var url = require('url')
var port = process.argv[2]

if(!port){
  console.log('请指定端口号好不啦？\nnode server.js 8888 这样不会吗？')
  process.exit(1)
}

var server = http.createServer(function(request, response){
  var parsedUrl = url.parse(request.url, true)
  var path = request.url 
  var pathNoQuery = parsedUrl.pathname
  var queryObject = parsedUrl.query
  var method = request.method
 
 /******** 从这里开始看，上面不要看 ************/

  console.log('HTTP 路径为\n' + path)
  if(path == '/pay'){
    response.setHeader('Content-Type', 'text/json')
    response.statusCode = 200 
    response.write(`
       {
           “张”:{
               “性别”：“男”，
               “年龄”：24
           }
       }
    `)
    response.end()
  }else{
    response.statusCode = 404
    response.end()
  }

  /******** 代码结束，下面不要看 ************/
})

server.listen(port)
console.log('监听 ' + port + ' 成功\n请用在空中转体720度然后用电饭煲打开 http://localhost:' + port)
```
当请求路径是/pay时，返回一串符合json格式的字符串。

### 前端ajax实现
``` javascript
button.addEventListener('click',(e)=>{
    let request = new XMLHttpRequest();
    request.open('GET','/pay'); //默认就是异步执行（请求类型，请求路径）
    request.send();//正式发送请求
    request.onreadystatechange = () => {
        if(request.readystate === 4){ //说明请求已经完成
            if(request.status === 200){ //说明请求返回，是成功的
                let object = JSON.parse(request.responseText); 
                console.log(object["张"][”性别“])；
            } 
        }
    } //如果请求的状态发生改变，则会执行当前函数，请求状态为0,1,2,3,4
}）
```
如果是XML格式的话，使用下面代码进行解析：
``` javascript
    let parser = new DOMParser();
    let XMLDoc = parser.parserFromString(request.responseText,"text/xml");
    XMLDoc.getElementsByTagName("content")[0].textContent;
```

### 通过XMLHttpRequest，完善http的请求与响应

#### 请求

``` http
GET /xxx HTTP/1.1
HOST: https://jack.com:8081
Content-type: x-www-form-urlencoded

我是第四部分
```
上面是一般http请求的组成结构，下面我们通过设置XMLHttpRequeset进行相应部分的设置。

``` javascript
    let request = new XMLHttpRequest();
    request.open('GET','https://jack.com:8081/xxx');
    request.setRequestHeader("Content-type","x-www-form-urlencoded");//header设置必须在open与send函数之间
    request.send("我是第四部分")
```
响应

``` http
HTTP/1.1 200 OK
Content-type: text/html

<!DOCTYPE html>
<html></html>
```
上面是http响应的一般组成结构，下面我们通过XMLHttpRequest进行相应部分的获取。

``` javascript 
 let status = request.status; //200
 let statusText = request.statusText; //OK
 let content = request.getResponseHeader("Content-type"); //text/html
 let allheader = request.getAllResponseHeaders();//获取全部的header 
 let Text = request.responseText; //第四部分
```