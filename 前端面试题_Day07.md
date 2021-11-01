# JavaScript

## 1. 执行栈与事件队列

当我们调用一个方法的时候，js会生成一个与这个方法对应的**执行环境**（context），又叫执行上下文。这个执行环境中存在着这个方法的私有作用域，上层作用域的指向，方法的参数，这个作用域中定义的变量以及这个作用域的this对象。

 而当一系列方法被依次调用的时候，因为js是单线程的，同一时间只能执行一个方法，于是这些方法被排队在一个单独的地方。这个地方被称为**执行栈**。

当一个脚本第一次执行的时候，js引擎会解析这段代码，并将其中的同步代码按照执行顺序加入执行栈中，然后从头开始执行。如果当前执行的是一个方法，那么js会向执行栈中添加这个方法的执行环境，然后进入这个执行环境继续执行其中的代码。当这个执行环境中的代码 执行完毕并返回结果后，js会退出这个执行环境并把这个执行环境销毁，回到上一个方法的执行环境。这个过程反复进行，直到执行栈中的代码全部执行完毕。

以上的过程说的都是**同步代码**的执行。

<hr>

那么当一个异步代码（如发送ajax请求数据）执行后会如何呢？前文提过，js的另一大特点是非阻塞，实现这一点的关键在于下面要说的这项机制——**事件队列**（Task Queue）。

js引擎遇到一个异步事件后并不会一直等待其返回结果，而是会将这个事件挂起，继续执行执行栈中的其他任务。当一个异步事件返回结果后，js会将这个事件加入与当前执行栈不同的另一个队列，我们称之为事件队列。**被放入事件队列不会立刻执行其回调，而是等待当前执行栈中的所有任务都执行完毕， 主线程处于闲置状态时，主线程会去查找事件队列是否有任务。**如果有，那么主线程会从中取出排在第一位的事件，并把这个事件对应的回调放入执行栈中，然后执行其中的同步代码...，如此反复，这样就形成了一个无限的循环。这就是这个过程被称为“事件循环（Event Loop）”的原因。

## 2. 运算符及优先级

| 运算符类型  | 含义                                                |
| ----------- | --------------------------------------------------- |
| 后置递增/减 |                                                     |
| 前置递增/减 |                                                     |
| **          | 幂                                                  |
| */%         | 乘除取余                                            |
| +           | 加法；字符串拼接。如'10'+3会得到'103'；隐式类型转换 |
| -           | 减法。如'103'-'1'会得到102                          |
|             | 大（小）于（等于）                                  |
| ===         | （严格）（不）相等                                  |
| &&          | 与                                                  |
| \|\|        | 或                                                  |
| ...?...:... | 三元运算符                                          |
| =           | 赋值                                                |
| ,           |                                                     |

## 3. call, apply, bind

call, apply, bind是函数的方法，用于改变this指向。

- call()方法调用一个对象。简单理解为调用函数的方式，但是它可以改变函数的this指向
- apply()方法调用一个对象。简单理解为调用函数的方式，但是它可以改变函数的this指向
- bind()方法不会调用函数。但是它可以改变函数的this指向

```javascript
let character = {
  name:'keqing',
  marry(person1,person2){
    console.log(`${this.name} loves ${person1} and ${person2}`);
  }
}
let me = {
  name:'traveller'
}
character.marry.call(me,'hutao','ganyu')
character.marry.apply(me,['yoimiya','keqing'])
let newMarry = character.marry.bind(me)
newMarry('sucrose','lisa')
```

主要应用场景是使用call实现（多重）继承，使用bind

## 4.正则表达式



## 5. var声明变量的提升

- 变量和函数的声明提升，但赋值不会提升
- 函数提升优先级高于变量提升

```javascript
var foo=function(x,y){
    return x-y;
}
function foo(x,y){
    return x+y;
}
var num=foo(1,2);
console.log(num);//结果是-1
// ----------------------原因在于上述代码等同于-----------------------
// 1.函数声明提升
function foo(x,y){
    return x+y
}
// 2.变量声明提升
var foo;
var num;
// 3.变量赋值不提升
foo = function(x,y){
    return x-y
}
num = foo(1,2)
console.log(num)
```



## 6. 继承

**构造函数继承**是每次继承都会把父类的所有属性方法全部拷贝一份，而对于公用的方法重复拷贝会浪费内存
**原型链继承**所有对象都公用一份原型属性和方法，对一个类的修改回影响的其他类
**组合继承**是结合两种继承方式，用**构造函数方式继承属性，原型链方式继承方法**

## 7. 对象调用

- 调用对象未声明的属性会undefined
- 调用对象已声明但未赋值的属性会报错
- 调用未声明的变量会报错
- 调用已声明但未赋值的变量会undefined

## 8. 同步与异步

- 异步事件
  - setTimeout
  - ajax
  - 文件加载
- js是单线程的，一个任务完成之后才能执行另一个任务
- **同步事件在运行栈中执行**完成后，执行**任务队列中的异步任务**
- process.nextTick(()=>{})：同步代码执行之后、异步代码执行之前执行
- setImmediate(()=>{})：当前事件循环结束，异步代码执行之后执行
- 异步程序要执行的代码是在时间到了的时候加入任务队列中的。如果此时运行栈中的同步代码已经执行完毕，那么就执行异步代码；如果同步代码没执行完，异步代码要等待。
- 事件循环：不断监测任务队列中是否存在异步程序，检测到时执行异步程序。这种机制叫做事件循环
- 宏任务：计时器、ajax、读取文件
- 微任务：Promise.then
- 执行顺序【一次事件循环】
  - 同步程序
  - Process.nextTick()
  - 异步程序
    - 微任务
    - 宏任务
  - setImmediate()

```javascript
process.nextTick(()=>{
  console.log(1);
})

console.log(2);

setTimeout(()=>{
  console.log(3);
},0)

setTimeout(()=>{
  console.log(6);
},1000)

setTimeout(()=>{
  console.log(7);
},0)

new Promise((resolve)=>{
  console.log(8);
  resolve()
}).then(()=>{
  console.log(9);
})

console.log(4);

setImmediate(()=>{
  console.log(5);
})
// 2,8,4,1,9,3,7,5,6
```



## 9. 冒泡

不能被冒泡的9个事件：

- load和unload 
- mouseenter和mouseleave 
- blur和focus 
- error 
- resize和abort

从3个角度说可分为ui事件、鼠标移入移出事件、聚焦和失焦事件

## 10. typeof 运算符

typeof 操作符返回一个**字符串**，表示未经计算的操作数的类型

| 类型                       | 结果：字符串 |
| -------------------------- | ------------ |
| Number                     | number       |
| NaN                        | number       |
| String                     | string       |
| Object                     | object       |
| null                       | object       |
| Array                      | object       |
| Function                   | function     |
| Undefined                  | undefined    |
| Boolean                    | boolean      |
| Symbol                     | symbol       |
| 除Function外的所有构造函数 | object       |

## 11. 生成器函数



## 12. 闭包

- 闭包是指有权访问另一个函数作用域中变量的函数
- 函数内再嵌套函数，返回到外部形成闭包
- 内部函数可以引用外层的参数和变量
- 参数和变量不会被垃圾回收机制回收

## 13. instanceof 运算符

instanceof 运算符用于检测**构造函数的 prototype 属性**是否出现在某个**实例对象的原型链**上

`object instanceof Constructor` 实例对象 instanceof 构造函数

如果对`Constructor.prototype`或者`object.__proto__`进行修改，那么之前用`new Constructor()`得到的实例对象object在进行`object instanceof Constructor`得到的结果就是false。

## 14. this

- 在不手动改变this指向的前提下，this总是指向函数的直接调用对象
- 如果有new关键字，this指向new出来的那个对象
- IE中attachEvent中的this总是指向全局对象window

## 15. Promise和async

```javascript
let p = new Promise((resolve)=>{
  console.log('my wife is');
  resolve('yoimiya')
})
p.then((data)=>{
  console.log(data);
})
```

- async 函数用于简化使用普通函数return Promise对象

- await 用于简化使用async函数时直接return resolve值，而不是正常使用时的Promise对象
- 【**普通函数返回Promise对象**用**async 函数**代替】
- 【**async函数执行返回Promise对象.then(data=>{})获取data**用**await Promise对象**代替】

```javascript
async function fn(){
  return 'hutao'
}
/*
function fn(){
  return new Promise((resolve)=>{
    resolve('hutao)
  })
}
*/
// async函数调用之后尽管里面return的是1，但实际上return的是Promise对象。写的return的值实际上是这个Promise对象.then传出的参数data
fn().then(res=>{
  console.log(`${res} is my girlfriend`);
})

//--------------------------------------
let p1 = new Promise((resolve)=>{
  resolve(1)
})
let p2 = new Promise((resolve)=>{
  resolve(2)
})
async function fun(){
  // 使用await可以省略上面Promise.then获取返回值的过程，直接得到写下的return的值
  let a = await p1
  let b = await p2
  console.log(a);
  console.log(b);
}
fun()
```

