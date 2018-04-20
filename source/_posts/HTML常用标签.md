---
title: HTML常用标签
date: 2018-03-27 12:03:56
tags:
---
## iframe标签
>      <iframe src="http://qq.com" frameborder="0"></iframe>
嵌入网页，frameboder="0",去除嵌入边框。
```    
        <iframe name=baidu src="#" frameborder="0"></iframe>
        <a href="http://baidu.com" target=baidu>baidu</a>
```
通过name跟target，实现点击链接，将网页嵌入iframe中。

*通过height和width设置宽高。*

## a标签
>     <a href="http://baidu.com" target="_blank" >baidu</a>
_blank在新标签窗口中打开；<br>
_self在当前窗口打开；<br>
_parent在父级窗口打开；<br>
_top在顶级窗口打开。<br>

>     <a href="http://baidu.com" download>baidu</a>
download属性，实现点击链接之后，浏览器直接进行下载，与Http中声明，Content-type:application/octet-stream效果一致。
### a标签的href属性解析
+ http://xxxxx
+ /Desktop||Desktop (路径，例如当前网址为https://127.0.0.1:8080,点击链接后，网址为https://127.0.0.1:8080/Desktop)
+ //qq.com (省略协议，协议与当前页面的协议一直，如果当前的html协议位file，则用file协议打开)
+ ?name=David (例如，https://127.0.0.1:8080?name=David)
+ javascript: alert(1); (伪协议，执行js语句，通常用javascript:;，实现点击之后不跳转)
+ \# (点击之后，会添加锚点，使得页面返回顶端)
+ ‘ ’ (为空时，点击会刷新页面)

## form标签
>       <form action="XXX?name=David" target="_blank" method="POST"></form>
action属性指定表单提交的地址，可以附带搜索项；method提交的方法POST,GET两种；target与a标签一致。<br>
**注意:表单中只有submit之后，才会提交。当form中，没有type=submit的input，而有button标签时，button标签会被提升为具有submit能力的按钮，type=button的input标签，在这种情况下，只为普通按钮。**

## input标签
+ submit <br>
样式为button，具有提交表单的能力。
+ button 
+ checkbox (复选框)
+ radio (单选框)
+ range (滑动条)
+ 还有很多(https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)

通常使用label标签，实现文字提示与input标签为整体，有如下两种方式:
>     <label>Click me <input type="text"></label>


>     <label for="username">Click me</label><input type="text" id="username">

## table标签
>     <table>
>       <colgroup>
>           <col style="background-color: #0f0">
>            <col span="2">
>        </colgroup>
>       <thead>表头</head>
>       <tbody>
>        <tr>
>            <th>Lime</th>
>            <th>Lemon</th>
>            <th>Orange</th>
>        </tr>
>        <tr>
>            <td>Green</td>
>            <td>Yellow</td>
>            <td>Orange</td>
>        </tr>
>        </tbody>
>        <tfoot>表尾</tfoot>
>        </table>