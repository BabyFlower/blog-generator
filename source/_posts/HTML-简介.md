---
title: HTML-简介
date: 2018-03-23 19:57:22
tags:
---
## W3C简介
万维网联盟（W3C）由蒂姆·伯纳斯-李（李爵士）于1994年10月离开欧洲核子研究中心（CERN）后成立，在欧盟执委会和国防高等研究计划署（DARPA）的支持下成立于麻省理工学院MIT计算机科学与人工智能实验室（MIT／LCS）。

W3C制定的标准包括HTML,CSS,XML,XHTML,DOM,SVG等。

## MDN简介
MDN Web Docs（旧称Mozilla Developer Network、Mozilla Developer Center，简称MDN）是一个汇集众多Mozilla基金会产品和网络技术开发文档的免费网站。
作为前端开发者，MDN是一个很好的查阅技术文档的网址。

## HTML的所有标签
### MAIN ROOT
+ html
### document metadata (页面信息)
+ link
+ meta (meta 元素表示那些不能由其它HTML元相关元素 (base, link, script, style 或 title) 之一表示的任何元数据信息，meta charset="utf-8")
+ style 
+ title
### sectioning root
+ body 
### content sectioning
+ address (contact information for a person or people, or for an organization)
+ article 
+ aside (表示一个和其余页面内容几乎无关的部分，被认为是独立于该内容的一部分并且可以被单独的拆分出来而不会使整体受影响。其通常表现为侧边栏或者嵌入内容)
+ footer 
+ header
+ h1-h6
+ hgroup (包含h1-h6标题的集合)
+ nav 
+ section (表示文档中的一个区域（或节），比如，内容中的一个专题组，一般来说会有包含一个标题（heading）)
### text content
+ blockquote
+ dir (已弃用)
+ div 
+ dd (用来指明一个描述列表  (dl) 元素中一个术语的描述。这个元素只能作为描述列表元素的子元素出现，并且必须跟着一个 dt 元素)
+ dl (是一个包含术语定义以及描述的列表，通常用于展示词汇表或者元数据 (键-值对列表))
+ dt (用于在一个定义列表中声明一个术语)

+ figure (代表一段独立的内容，与说明figcaption配合使用，这个标签经常是在主文中引用的图片，插图，表格，代码段等等)
+ figcaption 
+ hr (水平线)
+ ul (无序列表)
+ ol (有序列表)
+ li (列表元素)
+ main
+ p
+ pre (表示预定义格式文本。在该元素中的文本通常按照原文件中的编排，以等宽字体的形式展现出来，文本中的空白符（比如空格和换行符）都会显示出来。(紧跟在 pre 开始标签后的换行符也会被省略))
### Inline text semantics
+ a
+ abbr (代表缩写，并可选择提供一个完整的描述)
+ b (粗体显示)
+ bdi 
+ bdo (改变文本方向)
+ br (回车)
+ cite (引用)
+ code 
+ data
+ dfn (术语的定义)
+ em (需要用户着重阅读的内容)
+ i 
+ kbd
+ mark
+ q (短引用)
+ ruby (被用来展示东亚文字注音或字符注释)
+ rp
+ rt
+ rtc
+ s (使用删除线来渲染文本。使用 s 元素来表示不再相关，或者不再准确的事情)
+ samp (用于标识计算机程序输出)
+ small
+ span
+ strong
+ sub (定义了一个文本区域，出于排版的原因，与主要的文本相比，应该展示得更低并且更小)
+ sup (定义了一个文本区域，出于排版的原因，与主要的文本相比，应该展示得更高并且更小)
+ time
+ u
+ var 
+ wbr
### Image and multimedia    
+ area
+ audio
+ img
+ map
+ track (被当作媒体元素—audio 和 video的子元素来使用。它允许指定计时字幕（或者基于事件的数据），例如自动处理字幕)
+ video
### Embedded content
+ applet (标志着包含了Java的applet)
+ embed (将外部内容嵌入文档中的指定位置)
+ noembed (已经弃用)
+ object (表示引入一个外部资源，这个资源可能是一张图片，一个嵌入的浏览上下文，亦或是一个插件所使用的资源)
+ param (定义了 object的参数)
+ picture (是一个容器，用来为其内部特定的 img 元素提供多样的 source 元素)
+ source (可包含图片，视频，音频等多源媒体的空元素)
### Scripting
+ canvas (用来通过脚本（通常是JavaScript）绘制图形)
+ script
+ noscript (如果页面上的脚本类型不受支持或者当前在浏览器中关闭了脚本，则HTML noscript元素定义要插入的html部分)
### Demarcating edits
+ del (删除文字元素（del）表示已经从文档中删除的文本范围)
+ ins (定义已经被插入文档中的文本)
### Table content
+ caption (标题)
+ col
+ colgroup
+ table
+ tbody
+ td
+ tfoot
+ th
+ thead
+ tr
### Forms
+ button
+ datalist
+ fieldset
+ form
+ input
+ lable
+ legend
+ meter
+ optgroup
+ option
+ output
+ progress
+ select
+ textarea
### Interactive elements
+ details
+ dialog
+ menu
+ menuitem
+ summary
----------------

## 空标签简介
一个空元素（empty element）可能是 HTML，SVG，或者 MathML 里的一个不可能存在子节点（例如内嵌的元素或者元素内的文本）的element。

area,
base,
br,
col,
colgroup (when the span is present),
command,
embed,
hr,
img,
input,
keygen,
link,
meta,
param,
source,
track,
wbr.

## 可替换标签
可替换元素（replaced element）的展现不是由CSS来控制的。这些元素是一类 外观渲染独立于CSS的 外部对象。 典型的可替换元素有 img、 object、 video 和 表单元素，如textarea、 input 。 某些元素只在一些特殊情况下表现为可替换元素，例如 audio 和 canvas 。 通过 CSS content 属性来插入的对象 被称作 匿名可替换元素（anonymous replaced elements）。

