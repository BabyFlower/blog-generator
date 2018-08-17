---
title: jQuery实现简单登入注册
date: 2018-08-17 15:06:37
tags:
---
## 前言
这篇文章，只是简单的描述了登入与注册的流程，记录一些常见的问题。用node.js搭建的服务器，前端用jQuery框架

### 前端表单提交
``` javascript
    let $form = $('#signUpForm')
    $form.on('submit', (e)=>{
      e.preventDefault()  //取消submit的默认事件
      let hash = {}
      let need = ['email', 'password', 'password_confirmation']
      need.forEach((name)=>{
        let value = $form.find(`[name=${name}]`).val()
        hash[name] = value
      })  //获取表单信息

      $.post('/sign_up', hash)  //用jQuery封装好的post方法
        .then((response)=>{
          //成功执行下面代码
          console.log(response) 
        }, (request)=>{
          //失败执行下面代码
          let {errors} = request.responseJSON 
          //若服务器响应头包含，Content-type : text/json，
          //则jQuery中会自动转成与json格式一致的对象，
          //存在request.responseJSON
          if(errors.email && errors.email === 'invalid'){
            $form.find('[name="email"]').siblings('.error')
              .text('邮箱格式错误')
          }
        })
    })
```

### 服务器端获取post的请求体
``` javascript
function readBody(request){
  return new Promise((resolve, reject)=>{
    let body = []
    request.on('data', (chunk) => {
      body.push(chunk);
    }).on('end', () => {
      body = Buffer.concat(body).toString();
      resolve(body)
    })
  })
}    

if(path==='/sign_in' && method === 'POST'){
    readBody(request).then((body)=>{
      let strings = body.split('&') // ['email=1', 'password=2', 'password_confirmation=3']
      let hash = {}
      strings.forEach((string)=>{
        // string == 'email=1'
        let parts = string.split('=') // ['email', '1']
        let key = parts[0]
        let value = parts[1]
        hash[key] = decodeURIComponent(value) // hash['email'] = '1'
      })
      let {email, password} = hash
    }
}
```

### 一些细节问题
+ 如http的请求体中包含xxxyyy@qq.com，在传输时，会进行转码，将@字符，转成%40，所以当服务器端接收到请求体时，应该先用decodeURIComponent(request)进行转码。


