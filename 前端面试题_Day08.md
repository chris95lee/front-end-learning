# HTML

- cookie的有效时间默认为-1，如果不进行设置的话，就会默认**在浏览器会话关闭时结束**。可以通过setMaxAge()方法设置cookie的生命期。当setMaxAge(0)表示立刻删除该浏览器上指定的cookie

# JavaScript

## 1. 操作符

- 一元加操作符会把字符串转换成数值

## 2. 数组

- unshift()：首部添加
- shift()：首部删除
- push()：尾部添加
- pop()：尾部删除

## 3. prototype继承简例

```javascript
var A = {n:4399};
var B = function(){this.n = 9999};
var C = function(){var n = 8888};
// B,C函数都继承A
B.prototype = A;
C.prototype = A;
// 创建B构造函数的实例b，B中的this指向b，即b有一个属性n，值为9999
var b = new B();
// 创建C构造函数的实例c，C中没有this，c也就没有私有的n属性，只能继承A的n属性
var c = new C();
A.n++;
console.log(b.n);//9999
console.log(c.n);//4400
```

## 4. 阻止默认事件

阻止事件的默认动作：`event.preventDefault()`

阻止事件冒泡：`event.stopPropagation()`

彻底阻止事件：`event.stopImmediatePropagation()`

## 5. 页面的性能指标

- 白屏时间（first Paint Time）——用户从打开页面开始到页面开始有东西呈现为止
- 首屏时间——用户浏览器首屏内所有内容都呈现出来所花费的时间
- 用户可操作时间(dom Interactive)——用户可以进行正常的点击、输入等操作，默认可以统计domready时间，因为通常会在这时候绑定事件操作
- 总下载时间——页面所有资源都加载完成并呈现出来所花的时间，即页面 onload 的时间

## 6. 模块化

- AMD和CMD都是浏览器端的js模块化规范，分别由require.js和sea.js实现。 

- CommonJS是服务器端的js模块化规范，由NodeJS实现。

## 7. this补充

- **this的值要等到代码真正执行时才能确定**
- 在事件中，this指向触发这个事件的对象， 特殊的是，IE中的attachEvent中的this总是指向全局对象Window；
- this是函数运行时自动生成的一个内部对象，只能在函数内部使用；

## 8. noscript标签

noscript标签用来定义**在脚本未被执行时的替代内容**。也可以用在检测浏览器是否支持脚本，若不支持脚本则可以显示NOSCRIPT标签里的innerText

## 9. js全局函数

- 编码相关：escape()、unescape()、encodeURI()、decodeURI()、encodeURIComponent()、decodeURIComponent()

- 数据处理：Number()、String()
- 数字相关：isFinite()、isNaN()、parseFloat()、parseInt()
- 特殊：eval()

## 10. history对象

History 对象包含用户（在浏览器窗口中）访问过的 URL

- 属性
  - length：返回历史列表中的网址数
- 方法
  - back()：加载 history 列表中的前一个 URL
  - forward()：加载 history 列表中的下一个 URL
  - go()：加载 history 列表中的某个具体页面

## 11. 原型链

![原型链](D:\front-end-learning\04JS高阶\JS高级\02-构造函数和原型\原型链.png)

不仅仅是ES5的构造函数，ES6的类同样可以调用prototype获得原型对象。

ES6，类可以通过extends和super实现继承。

ES5，需要使用原型对象实现继承。

![借用原型对象继承方法](D:\front-end-learning\04JS高阶\JS高级\02-构造函数和原型\借用原型对象继承方法.png)

## 12. 类、构造函数、继承【代码】

