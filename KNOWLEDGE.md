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

### 原型 原型链 作用域 作用域链 构造函数 new

原型继承 (prototypal inheritance) 

```js
obj.__proto__ === Object.prototype
```

1、Object.prototype 2、Function.prototype 3、寄生组合继承
DOM、attributes是属于property的一个子集、attribute和property之间的数据绑定是单向的，attribute->property；更改property和attribute上的任意值，都会将更新反映到HTML页面中；

静态方法、私有方法、Getters、Setters

#### js的new操作符做了哪些事情

```js
var obj = new Base();

// new 操作符解析

// 1、创建一个空的对象
var obj = new Object();
// 2、链接到原型
obj.__proto__= Base.prototype;
// 3、绑定this指向，执行构造函数
var result = Base.call(obj);
// 4、确保返回的是对象
if (typeof(result) == "object"){
    func=result;
}else{
    func=obj;;
}

/*
  create函数要接受不定量的参数，第一个参数是构造函数（也就是new操作符的目标函数），其余参数被构造函数使用。
  new Create() 是一种js语法糖。我们可以用函数调用的方式模拟实现
*/
function create(Con,...args){
    //1、创建一个空的对象
    let obj = {}; // let obj = Object.create({});
    //2、将空对象的原型prototype指向构造函数的原型
    Object.setPrototypeOf(obj,Con.prototype); // obj.__proto__ = Con.prototype
    //3、改变构造函数的上下文（this）,并将剩余的参数传入
    let result = Con.apply(obj,args);
    //4、在构造函数有返回值的情况进行判断
    return result instanceof Object?result:obj;
}
```



DOMContentLoaded、

use strict：限制with、全局变量、this、变量不规范

SPA和SEO：Todo PhantomJS 

JS调试: log\break

Todo (function() { /* jQuery plugin code referencing */ } )(jQuery)

拷贝与深拷贝：循环遍历对象的属性赋值、ES6的Object.assign、ES6扩展运算符、JSON.parse(JSON.stringify(obj))、手动递归；immutable

### 数据类型

基本类型: 5+1+1 、null、undefined、String、Number、Boolean、Object、Symbol

判断数据类型: typeof、instanceof、isArray、Object.prototype.toString.call、Reflect.toString.call

数据结构、不可变数据、getOwnProperty

##### 对象的数据属性

- configurable:false, // 能否使用delete、能否需改属性特性、或能否修改访问器属性、，false为不可重新定义，默认值为true
- enumerable:false, // 对象属性是否可通过for-in循环，flase为不可循环，默认值为true
- writable:false, // 对象属性是否可修改,flase为不可修改，默认值为true
- value:'value' // 对象属性的默认值，默认值为undefined

##### 访问器属性

- getter

- setter

##### 对象方法：defineProperty、getOwnPropertyNames、getOwnPropertyDescriptor、defineProperties、

#### 遍历

1.for...in；2.Object.keys(obj)；3.Object.getOwnPropertyNames(obj)；4.Object.getOwnPropertySymbols(obj)；5.Reflect.ownKeys(obj)；

#### 闭包 (closure)

##### 定义：闭包是指有权访问另一个函数作用域中的变量的函数。数学：集合进行运算时封闭的空间。

##### 原理：通过函数作用域链实现。

##### 作用：数据缓存、封装、隔离作用域。

①函数嵌套函数

②函数内部可以引用函数外部的参数和变量

③参数和变量不会被垃圾回收机制回收

```js
// closure
function space() {
  var param = {attribute: 1}
  function closure() {
    console.log('param ', param) // 使用外部变量
  }
}

```





### 体验优化

图片预加载、懒加载

### 性能优化

### JS模块化

CommonJS（nodejs）、AMD（requirejs）、CMD(seajs)、UMD、ES6 Module

```js
// AMD
// Global
require.config({
    paths:{
        "jquery":'../lib/jquery.min'
    }
});
// define
define([dep], function() {
  return object
})
// use
require([object], function(obj) {
  obj.xxx
})

// CMD
define(function(require, exports, module) {
  // 模块代码
  // 异步加载多个模块，在加载完成时，执行回调
  require.async(['./c', './d'], function(c, d) {
    c.doSomething();
    d.doSomething();
  });
  // 使用模块系统内部的路径解析机制来解析并返回模块路径
  console.log(require.resolve('./b')
});
  
// UMD
(function(root, factory) {
  if (typeof module === 'object' && typeof module.exports === 'object') {
    // 是commonjs模块规范，nodejs环境
    var depModule = require('./umd-module-depended')
    module.exports = factory(depModule);
  } else if (typeof define === 'function' && define.amd) {
    // 是AMD模块规范，如require.js
    define(['depModule'], factory)
  } else if (typeof define === 'function' && define.cmd) {
    // 是CMD模块规范，如sea.js
    define(function(require, exports, module) {
      var depModule = require('depModule')
      module.exports = factory(depModule)
    })
  } else {
    // 没有模块环境，直接挂载在全局对象上
    root.umdModule = factory(root.depModule);
  }
}(this, function(depModule) {
  console.log('我调用了依赖模块', depModule)
  return {
    name: '我自己是一个umd模块'
  }
}))
```



### 算法

#### 数组去重

```js
// Object.keys
for(var i = 0; i < array.length; i++) {
  values[array[i]] = null;
}
Object.keys(values)

// array.reduce
// 1
array.reduce(function(ret, cur) {
  if(ret.indexOf(cur) === -1) ret.push(cur);
  return ret;
}, []);
// 2
let arr = array.reduce((accumulator, current) => {
    return accumulator.includes(current) ? accumulator : accumulator.concat(current);
}, []);

// array.filter
let arr = array.filter((item, index, arr) => arr.indexOf(item) === index);

// new Set
let arr = [...new Set(array)];

// 递归、双循环、额外存储空间

```





Todo 算法:字符串数据、数据处理、对象处理、遍历

Worker API

跨域 - JSONP、domain（子域访问父域）、postMessage、反向代理、cors（跨域资源共享机制）

web存储 - cookie、storage、indexedDB

### javaScript的执行分为：解释和执行两个阶段。

解释阶段：词法分析、语法分析、作用域规则确定；

执行阶段：创建执行上下文、执行函数代码、垃圾回收。

### 其他

##### 浮点精度: 二进制无法精确表示”浮点数和大于2^53次的整数“，二进制0舍1入，导致精度丢失。简易方法：放大成整数，再缩小。





# 工程化

打造完整开发流程

### 规范化

- 目录结构的制定
- 编码规范
- 前后端接口规范
- 文档规范
- 协作工具，开发工具
- 组件管理
- Git分支管理
- Commit描述规范
- 定期CodeReview
- 视觉图标规范
- 开发环境规范
- Docker+k8s
- CLI



### 自动化

- 自动图标合并，涉及到css sprite，svg sprite，图标字体
- 自动编写可视化文档，技术选型：postmark+jsdoc
- 自动化测试，技术选型：Karma + Mocha + Expect.js
- 自动化部署，技术选型：docker
- 自动化问题反馈

CI

CD

### 模块化

框架性能体验优化

- js的模块化
- css的模块化
- 资源的模块化

### 组件化

组件库



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

#### Promise

#### Array

```js
array.reduce(function(total, currentValue, currentIndex, arr), initialValue)
```

#### 箭头函数

1. 箭头函数没有`prototype`(原型)
2. 箭头函数的this在定义的时候继承自外层第一个普通函数的this。
3. 如果箭头函数外层没有普通函数，严格模式和非严格模式下它的this都会指向`window`(全局对象)
4. 箭头函数本身的this指向不能改变，但可以修改它要继承的对象的this。
5. 箭头函数的this指向全局，使用arguments会报未声明的错误。
6. 箭头函数的this指向普通函数时,它的`argumens`继承于该普通函数
7. 使用`new`调用箭头函数会报错，因为箭头函数没有`constructor`
8. 箭头函数不支持`new.target`
9. 箭头函数不支持重命名函数参数,普通函数的函数参数支持重命名
10. 箭头函数相对于普通函数语法更简洁优雅

主要分为这几个方面的区别： 1、this指向 2、arguments 3、箭头函数没有原型 4、箭头函数不能使用new来构造 5、不允许重命名参数 6、语法更优雅 7、 不支持new.target

**箭头函数的注意事项**：

1. 箭头函数一条语句返回对象字面量，需要加括号
2. 箭头函数在参数和箭头之间不能换行
3. 箭头函数的解析顺序相对`||`靠前
4. 函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象。





# Todo
# React
# Vue
# Webpakc
# Node

# 团队建设：周会、团建、code review、掘金输出文档、重构消除技术负债、招贤纳士、面试经验

