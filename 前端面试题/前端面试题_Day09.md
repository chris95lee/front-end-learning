## 1. window的open方法

open() 方法可以查找一个已经存在或者新建的浏览器窗口。

**语法：**

window.open([URL], [窗口名称], [参数字符串])

**参数说明:**

URL：可选参数，在窗口中要显示网页的网址或路径。如果省略这个参数，或者它的值是空字符串，那么窗口就不显示任何文档。

窗口名称：可选参数，被打开窗口的名称。

  1.该名称由字母、数字和下划线字符组成。
  2."_top"、"_blank"、"_selft"具有特殊意义的名称。
    _blank：在新窗口显示目标网页
    _self：在当前窗口显示目标网页
    _top：框架网页中在上部窗口中显示目标网页
  3.相同 name 的窗口只能创建一个，要想创建多个窗口则 name 不能相同。
  4.name 不能包含有空格。

参数字符串：可选参数，设置窗口参数，各参数用逗号隔开。

## 2. ==和===

相等运算符==会进行类型转换，再进行比较

- null == undefined【true】
- 数字 == 字符串【把字符串转换为数字，再进行比较】
- ==的参数如果是true，则把true转换为数字1；反之如果是false，则转换为数字0
- NaN表示非数字值，特殊之处：它和任何值都不相等，包括自身。

## 3. 隐式转换

+：数字隐式转换为字符串

-*/%：字符串隐式转换为数字

## 4. DOM获取元素

getElementById

getElementsByTagName

getElementsByClassName

getElementsByName

## 5. 跨域

- 第一种方式：jsonp请求；jsonp的原理是利用<script>标签的跨域特性，可以不受限制地从其他域中加载资源，类似的标签还有<img>.
- 第二种方式：document.domain；这种方式用在主域名相同子域名不同的跨域访问中
- 第三种方式：window.name；window的name属性有个特征：在一个窗口(window)的生命周期内,窗口载入的所有的页面都是共享一个window.name的，每个页面对window.name都有读写的权限，window.name是持久存在一个窗口载入过的所有页面中的，并不会因新页面的载入而进行重置。
- 第四种方式：window.postMessage；window.postMessages是html5中实现跨域访问的一种新方式，可以使用它来向其它的window对象发送消息，无论这个window对象是属于同源或不同源。
- 第五种方式：CORS；CORS背后的基本思想，就是使用自定义的HTTP头部让浏览器与服务器进行沟通，从而决定请求或响应是应该成功还是应该失败。
- 第六种方式：Web Sockets；web sockets原理：在JS创建了web socket之后，会有一个HTTP请求发送到浏览器以发起连接。取得服务器响应后，建立的连接会使用HTTP升级从HTTP协议交换为web sockt协议。

## 6. 数组

- sort()：在原数组上进行排序，不生成副本

```javascript
// array.sort(sortfunction)比值函数
array.sort(function(a, b){return a - b})// 升序
array.sort(function(a, b){return b - a})// 降序
/* 
比较函数应该返回一个负，零或正值，这取决于参数：当 sort() 函数比较两个值时，会将值发送到比较函数，并根据所返回的值（负、零或正值）对这些值进行排序。
*/
```

- toString() 把数组转换为数组值（逗号分隔）的字符串
- oin()可将所有数组元素结合为一个字符串，可规定分隔符
- pop()从数组中删除最后一个元素，返回值是被删除的元素
- push()在数组结尾添加一个元素，返回值是新数组的长度
- shift()从数组中删除第一个元素，返回值是被删除的元素
- unshift()在数组开头添加一个元素，返回值是新数组的长度
- splice()
- concat()方法通过合并（连接）现有数组来创建一个新数组。不改变原数组
- slice()从开始参数选取元素，直到结束参数（不包括）为止切出新数组。不改变原数组

## 7. 其他

- JavaScript内部，所有数字都是以64位浮点数形式储存，即使整数也是如此

- typeof null === 'object' //true

  null instanceof Object //false
