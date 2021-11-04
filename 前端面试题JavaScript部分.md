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



## 14. 构造函数、类、继承



## 15. call、apply、bind



## 16. 正则表达式



## 17. 原型链



## 18. BOM