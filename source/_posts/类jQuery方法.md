---
title: 类jQuery方法
date: 2018-04-26 22:07:22
tags:
---
``` javascript
window.jQuery = function(node){
    let elements = document.getElementsByTagName(node);
    let elementSet = {
        node : elements
    }
    elementSet.addClass  =  function(classes){
        for(let i=0; i < elements.length;i++){
            elements[i].classList.add(classes);
        }
    }
    elementSet.textSet = function(text){
        for(let i =0; i < elements.length;i++){
            elements[i].textContent = text;
        }
    }
    return elementSet;
}

window.$ = jQuery

var $div = $('div')
$div.addClass('red') // 可将所有 div 的 class 添加一个 red
$div.setText('hi') // 可将所有 div 的 textContent 变为 hi

```

1. 定义一个构造函数jQuery，并返回具有各种属性和方法的对象。
2. 通过调用jQuery，能够实例化对象，执行相关的方法。
