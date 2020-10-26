# HTML

"<!doctype>"

生命周期:cookie 的生命周期由服务器控制，默认是关闭浏览器后删除；sessionStorage 仅在当前的窗口有效，localStorage 除非手动删除否则一直存在。

http 通信:浏览器每次向服务器发送请求的时候都要带上该域的 cookie，而 sessionStorage 和 localStorage 仅存在于浏览器端。

作用域:cookie 和 localStorage 在同个域名下的多个窗口都有效，sessionStorage 只在一个窗口有效，不能跨窗口共享。

css放在head中： css放在head中， 是因为浏览器解析html文档是自上而下的，如果放底部的话，页面结构出来了，css还没开始渲染，可能会看到只有结构的页面。 CSS 应当写在 head 中，以避免页面元素由于样式确实造成瞬间的白页或者给用户闪烁感。 

js放在/body之前： JS可能会改变DOM树，也可能依赖css样式。如果放在前面，那么DOM和css可能还未加载，这样容易报错。 性能：js放前面，页面会先去加载他，拖慢了时间，使用户在一定时间内看不到网页内容。例外：js如果需要先加载后运行可以写在头里（当脚本使用 defer 方式加载的时候可以不用约束放置的位置。）


# CSS

清除浮动 -- :after {clear:both;content:’.’;display:block;width: 0;height: 0;visibility:hidden;}

BFC --- 1.BFC区域不会与float box重叠 2.BFC是页面上的一个独立容器，子元素不会影响到外面 3.计算BFC的高度时，浮动元素也会参与计算

1.根元素 2.float属性不为none 3.position为absolute或fixed 4.display为inline-block, table-cell, table-caption, flex, inline-flex 5.overflow不为visible
CSS sprites
兼容性 reset.css normalize.css
CSSOM -- ele.style[apis] \ document.styleSheets \ document.styleSheets[0].cssRules
W3C盒子模型——属性高（height）和属性宽（width）这两个值不包含（padding）和（border）
IE盒子模型——属性高（height）和属性宽（width）这两个值包含（padding）和（border）
! important> 内联样式 1000>id 100> 类、伪类、属性选择器 10>元素、伪元素选择器>*>继承
可继承的属性：font-size, font-family, color

"<head>里边<link rel=”stylesheet” type=”text/css” href=”xxx.css” media=”only screen and (max-device-width:480px)”>
CSS : @media only screen and (max-device-width:480px) {/css样式/}"

避免过度约束避免后代选择符避免链式选择符使用紧凑的语法避免不必要的命名空间避免不必要的重复最好使用表示语义的名字

当按百分比设定一个元素的宽度时，它是相对于父容器的宽度计算的，包括margin、padding
基本原理是通过媒体查询检测不同的设备屏幕尺寸做处理。

页面头部必须有meta声明的viewport。

布局：多列-浮动、box-sizing、position；居中：margin、负margin、table-cell（vertical-align: middle; text-align: center;）、flex（align-items: center;justify-content: center;）

多行元素的文本省略号：text-overflow: ellipsis;

减少重绘与回流

# JS

事件代理 (event delegation)、声明提升、事件冒泡、事件机制、事件循环（event loop）

this指针：全局、调用对象、构造对象、call/apply/bind第一个参数

原型继承 (prototypal inheritance) ---- obj.__proto__ === Object.prototype
1、Object.prototype 2、Function.prototype 3、寄生组合继承
DOM、attributes是属于property的一个子集、attribute和property之间的数据绑定是单向的，attribute->property；更改property和attribute上的任意值，都会将更新反映到HTML页面中；

DOMContentLoaded、

use strict：限制with、全局变量、this、变量不规范
SPA和SEO：Todo PhantomJS \\ JS调试: log\break

Todo (function() { /* jQuery plugin code referencing */ } )(jQuery)

拷贝与深拷贝：循环遍历对象的属性赋值、ES6的Object.assign、ES6扩展运算符、JSON.parse(JSON.stringify(obj))、手动递归；immutable

数据类型、数据结构、不可变数据、getOwnProperty

Todo 闭包 (closure)

Todo 算法:字符串数据、数据处理、对象处理、遍历、

Worker API

# 网络

http2.0 \ 跨域 \ proxy配置

# 安全

转码 escape encodeURI encodeURIComponent  \加密

# ESnext

Proxy、Reflect、Set && Map、Symbol、Destructuring、async
EX6
EX7
EX8
EX9
EX10
EX11：matchAll、动态导入、import.meta、export * as ns from 'module'、Promise.allSettled、BigInt、GlobalThis、??、?.

# Todo
# React
# Vue
# Webpakc
# Node

# 团队建设：周会、团建、code review、掘金输出文档、重构消除技术负债、招贤纳士、面试经验

