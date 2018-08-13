---
title: Promise
date: 2018-08-13 16:23:50
tags:
---
## 自己封装的jQuery.ajax
``` javascript
window.jQuery = function(nodeOrSelector){
  let nodes = {}
  nodes.addClass = function(){}
  nodes.html = function(){}
  return nodes
}
window.$ = window.jQuery

window.jQuery.ajax = function({url, method, body, successFn, failFn, headers}){
  let request = new XMLHttpRequest()
  request.open(method, url) // 配置request
  for(let key in headers) {
    let value = headers[key]
    request.setRequestHeader(key, value)
  }
  request.onreadystatechange = ()=>{
    if(request.readyState === 4){
      if(request.status >= 200 && request.status < 300){
        successFn.call(undefined, request.responseText)
      }else if(request.status >= 400){
        failFn.call(undefined, request)
      }
    }
  }
  request.send(body)
}
```
如果要准确执行上述的ajax函数，我们必须知道其中成功与失败的回调函数的位置或者相应的属性名。这就表明对于一些封装好的函数，为了能够正常使用，我们需要看它的文档。

``` javascript
function f1(responseText){}
function f2(responseText){}

myButton.addEventListener('click', (e)=>{
  window.jQuery.ajax({
    url: '/frank',
    method: 'get',
    headers: {
      'content-type':'application/x-www-form-urlencoded',
      'frank': '18'
    },
    successFn: (x)=>{
      f1.call(undefined,x)
      f2.call(undefined,x)
    },
    failFn: (x)=>{
      console.log(x)
      console.log(x.status)
      console.log(x.responseText)
    }
  })
})
```

## 再来看看实际jQuer.ajax
``` javascript
    $.ajax({
        url: '/frank',
        method: 'get',
        headers: {
        'content-type':'application/x-www-form-urlencoded',
        'frank': '18'
        }
    }).then(success,fail);

    function success(x){
       f1.call(undefined,x)
       f2.call(undefined,x)       
    }

    function fail(){
      console.log(x)
      console.log(x.status)
      console.log(x.responseText)
    }
```
实际jQuery的ajax用promise进行了封装，then()里面传递成功与失败的回调函数，不需要去查看文档。**所以promise第一个好处是确定了一种规范。**

## Promise可以对结果进行链式处理

``` javascript
    $.ajax({}).then(f1,f2).then(f3,f4).then()......
```
每一次then()处理完返回的数据，也是一个promise的实例，可以对于返回的结果，再一次进行then()。

## 用promise自己封装ajax

简单的使用一下promis：

``` javascript
   let promise = function(argument){
       return new Promise(function(resolve,reject){
           //成功的话
           resolve,call(undefined,argument);
           //失败的话
           reject.call(undefined,argument);
       })
   } 

   promise.then(()=>{},()=>{}); //传递两个函数，第一个为成功，第二个为失败即可。

```
将自己编写的ajax用promise封装如下：

``` javascript
window.jQuery = function(nodeOrSelector){
  let nodes = {}
  nodes.addClass = function(){}
  nodes.html = function(){}
  return nodes
}
window.$ = window.jQuery

window.Promise = function(fn){
  // ...
  return {
    then: function(){}
  }
}

window.jQuery.ajax = function({url, method, body, headers}){
  return new Promise(function(resolve, reject){
    let request = new XMLHttpRequest()
    request.open(method, url) // 配置request
    for(let key in headers) {
      let value = headers[key]
      request.setRequestHeader(key, value)
    }
    request.onreadystatechange = ()=>{
      if(request.readyState === 4){
        if(request.status >= 200 && request.status < 300){
          resolve.call(undefined, request.responseText)
        }else if(request.status >= 400){
          reject.call(undefined, request)
        }
      }
    }
    request.send(body)
  })
}

myButton.addEventListener('click', (e)=>{
  let promise = window.jQuery.ajax({
    url: '/xxx',
    method: 'get',
    headers: {
      'content-type':'application/ruxiax-www-form-urlencoded',
      'frank': '18'
    }
  })

  promise.then(
    (text)=>{console.log(text)},
    (request)=>{console.log(request)}
  )

})

```

