---
title: jsonp简介
date: 2018-05-19 11:54:49
tags:
---
# what is JSONP
JSONP（JSON with Padding）是数据格式JSON的一种“使用模式”，可以让网页从别的网域要数据。
利用script元素的这个开放策略，网页可以得到从其他来源动态产生的JSON数据，而这种使用模式就是所谓的JSONP。用JSONP抓到的数据并不是JSON，而是任意的JavaScript，用JavaScript解释器运行而不是用JSON解析器解析。

简单来说：JSONP利用动态的创建script标签，来获取其他网站的数据。由于script标签获取的方式是GET，所以JSONP只能支持GET。

## 响应服务器端实现（node.js）
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
  var query = ''
  if(path.indexOf('?') >= 0){ query = path.substring(path.indexOf('?')) }
  var pathNoQuery = parsedUrl.pathname
  var queryObject = parsedUrl.query
  var method = request.method
 
 /******** 从这里开始看，上面不要看 ************/

  console.log('HTTP 路径为\n' + path)
  if(path == '/style.css'){
    response.setHeader('Content-Type', 'text/css; charset=utf-8')
    response.write('body{background-color: #ddd;}h1{color: red;}')
    response.end()
  }else if(path == '/main.js'){
    response.setHeader('Content-Type', 'text/javascript; charset=utf-8')
    response.write('alert("这是JS执行的")')
    response.end()
  }else if(path == '/pay'){
    response.setHeader('Content-Type', 'application/javascript')
    response.statusCode = 200 
    response.write(`${query.callback}.call(undefined,'success')`)
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
主要部分在/pay，定义httpHeader，Content-Type : application/javascript。
http的内容部分为js的回调函数，函数名存于callback，如果需要返回数据，则添加到函数参数中。
当浏览器接收到返回数据，则会执行该js语句。

## 网页实现
``` javascript
  button.addEventListener('click',(e)=>{
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
      e.currentTarget.remove(); //当script加载成功时，把标签移除
      delete window[functionName] //移除全局的回调函数      
    }
  })
```
主要是构造一个全局的回调函数。在script加载之后，执行回调。

### 用jQuery实现
``` javascript
  $.ajax({
    url : 'http://127.0.0.1:8080/pay',
    dataType : "jsonp",
    success :  function(response){
      if(response === "success"){
        alert('success')
      }
    }
  })
```
