# JavaScript面试题整理

## 1. var let

### 1.1 var

var声明的变量会自动提升到所在作用域的顶部，但是只提升声明，不提升赋值。

`function fn(){}`进行函数定义也会实现声明提升

但`var fn = function(data){}`只会提升var fn，其余代码`fn = function(data){}`不会改变位置

### 1.2 let

let声明的范围是块级作用域，声明的变量不会在作用域中提升，因此存在暂时性死区。

let在全局作用域中声明的变量不会称为window对象的属性，var则会

## 2. 数据类型

| 数据类型      | 值                                     | typeof         | 详细                                                         |
| ------------- | -------------------------------------- | -------------- | ------------------------------------------------------------ |
| **Undefined** | undefined                              | 'undefined'    | var或let声明变量，但未初始化赋值。<br />声明但未初始化 和 未声明 是不同的 |
| 未声明的变量  |                                        | 'undefined'    |                                                              |
| **Null**      | null                                   | 'object'       | 空对象指针。let car = null                                   |
|               |                                        |                | undefined派生于null，null==undefined // true                 |
| **Boolean**   | true, false                            |                | **将其他类型的值转换为布尔值Boolean()**                      |
|               | **Boolean()**                          | false          | false, '', 0, NaN, null, undefined                           |
|               |                                        | true           | true, 非空字符串, 非零数值, 任意对象                         |
| **Number**    | 整数, 浮点值, Infinity, -Infinity, NaN |                | NaN不等于包括自身的任何值                                    |
|               | **Number()**                           | 1              | true                                                         |
|               |                                        | 0              | false, null, ''                                              |
|               |                                        | NaN            | undefined, 其他字符串                                        |
| **String**    |                                        |                |                                                              |
|               | **toString()**                         | 'null'         | null                                                         |
|               |                                        | 'undefined'    | undefined                                                    |
|               |                                        | 'true'/'false' | true/false                                                   |
| **Symbol**    |                                        |                |                                                              |
| **Object**    |                                        |                |                                                              |



## 3. 操作符

### 3.1 相等操作符

| 等于== 不等于!=       | 先进行类型转换                      | 再确定操作数是否相等 |
| --------------------- | ----------------------------------- | -------------------- |
| 布尔值                | false转换为0，true转换为1           |                      |
| 字符串==数值          | 字符串转换为数值                    |                      |
| 对象                  | 调用对象的valueOf()方法取得其原始值 |                      |
| null, undefined       | 不能转换为其他类型的值              |                      |
| 对象 == 对象          | 比较是不是指向同一个对象            |                      |
| NaN == 任何值         | NaN不等于任何值，包括NaN            | false                |
| NaN != 任何值         | NaN不等于任何值，包括NaN            | true                 |
| null == undefined     |                                     | true                 |
| false == 0            |                                     | true                 |
| true == 1             |                                     | true                 |
| true ==2              |                                     | false                |
| undefined == 0        |                                     | false                |
| null == 0             |                                     | false                |
| **全等于===** **!==** |                                     |                      |
| null === undefined    |                                     | false                |

## 4. 变量、作用域与内存

变量包含两种不同类型的数据

### 4.1 原始值与引用值

**原始值**：最简单的数据（Number, String, Boolean, Null, Undefined, Symbol）

保存原始值的变量是按值访问的，操作的就是存储在变量中的实际值。

通过变量把一个原始值赋值到另一个变量，原始值会被复制到新变量的位置。

**引用值**：多个值构成的对象（Object）

保存引用值的变量是按引用访问的，操作的就是存储在变量中的引用。

把引用值从一个变量赋给另一个变量时，存储在变量中的值也会被复制到新变量所在的位置，但这里复制的值实际是一个指针，指向存储在堆内存中的对象。两个变量指向同一个对象，一个对象上面的变化会在另一个对象上反映。

#### 4.1.1 传递参数

**ECMAScript中所有函数传递参数都是按值传递的**，没有按引用传递的。

**按值传递参数**：值会被复制到函数的参数，即一个局部变量上。

**按引用传递参数**：值在内存中的位置会被保存在一个局部变量，意味着对本地变量的修改会反映到函数外部。【js不采用】

```javascript
// 传递的参数是原始值，按值传递
function addTen(num){
  num+=10
  return num
}
let count = 20
let result = addTen(count)
console.log(count);
console.log(result);
// 传递的参数是引用值，按值传递
function setName(obj){
  obj.name = 'hutao'
}
let person = new Object()
setName(person)
console.log(person.name);
// 按值传递，而非按引用传递
function setName2(obj){
  /* 这里传入形参obj的值是实参person2的值，也就是存放在栈内存的地址，这个地址指向存放在堆内存的对象。因此形参和实参都指向同一个对象，对形参的name属性赋值，也会影响实参person2*/
  obj.name = 'hutao'
  /*但是这里，形参obj被赋值了一个新的对象，也就是说obj的值是一个新对象的地址，不同于person2的地址了，所以添加的name属性也不会影响person2*/
  obj = new Object()
  obj.name = 'yoimiya'
  return obj
}
let person2 = new Object()
let newObj = setName2(person2)
console.log(person2.name);
console.log(newObj.name);
```

### 4.2 typeof和instanceof

| typeof     | 适合判断一个变量是否是原始类型 |
| ---------- | ------------------------------ |
| instanceof | 判断一个引用值是什么类型的对象 |

### 4.3 执行上下文和作用域

变量和函数的上下文决定了它们可以访问哪些数据，以及它们的行为。每个上下文都有一个关联的变量对象，而这个上下文中定义的所有变量和函数都存在于这个对象上。

全局上下文是最外层的上下文，在浏览器中，全局上下文是window对象。

**var变量声明提升**：**var声明**会被拿到函数或全局作用域的顶部，位于作用域所有代码之前。

### 4.4 垃圾回收

javascript通过自动内存管理实现内存分配和闲置资源回收：确定哪个变量不再使用，然后释放它占用的内存。这个过程是周期性的，即垃圾回收程序每隔一段时间自动运行。垃圾回收程序必须跟踪哪个变量还会使用，哪个不再使用，以便释放内存。

JavaScript的垃圾回收策略

#### 4.4.1 标记清理【常用】

#### 4.4.2 引用计数【不常用】

#### 4.4.3 性能与内存管理

1. const和let提升性能
2. 内存泄漏
   1. 意外声明全局变量
   2. 定时器
   3. 闭包
3. 隐藏类和删除操作

## 4. DOM



## 5. 跨域



## 6. 浏览器的解析和渲染

### 6.1 DOM树和渲染树



### 6.2 重绘repaint和重排（回流）reflow



## 7. 线程



## 8. 事件



## 9. Window对象



## 10. 同步与异步



## 11. 执行栈与事件队列



## 12. Promise和async



## 13. this

### 13.1 普通函数中的this

普通函数`funtion(){}`无论是作为函数的定义，或是对象中的方法，其函数体内的this指向调用这个函数或方法的对象。

### 13.2 箭头函数中的this

箭头函数`()=>{}`函数体内的this指向由这个箭头函数在哪里定义决定的。

### 13.3 立即执行函数中的this

立即执行函数`(function(){})()或(function(){}())`实际是由window对象调用的。因此其函数体内的this指向window

```javascript
var myObject = {
    foo: "bar",
    func: function() {
        var self = this;
        console.log(this.foo);   
        console.log(self.foo);   
        (function() {
            console.log(this.foo);   
            console.log(self.foo);   
        }());
    }
};
myObject.func();
```



## 14. 构造函数、类、继承



## 15. call、apply、bind



## 16. 正则表达式



## 17. 原型链



## 18. BOM



## 19. Web应用作用域

Web程序对象作用域常用的有三个：**请求作用域，会话作用域，应用上下文**。 请求作用域req范围最小，需要的资源最少，作用当前请求 session会话作用于本次对话，每个对话都有JSessionID， ServletContext作用域范围大：web应用中所有都能够访问，生命周期和web容器一样长，维护所需资源多。 在满足需求内耗费的资源越小越好

## 20. 数组的sort方法

```javascript
let arr = [3,15,8,28,32,22]
console.log(arr.sort());
// 升序
console.log(arr.sort(function(a,b){return a-b}));
// 降序
console.log(arr.sort(function(a,b){return b-a}));
// 数据经过一定处理后的结果按升序确定顺序后，按这个顺序排列原数据
console.log(arr.sort(function(a,b){return Math.abs(a-17)-Math.abs(b-17)}));
```

