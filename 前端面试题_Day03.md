# HTML

## 1. 标签及属性

- `<input>`的multiple属性用于在input的type='file'时，上传文件可设置多选

- `<a href=""><button></button></a>`a标签内嵌套button标签

- `<optgroup></optgroup>`用于组合选项。当您使用一个长的选项列表时，对相关的选项进行组合会使处理更加容易。

  ```html
  <select>
    <optgroup label="Swedish Cars">
      <option value="volvo">Volvo</option>
      <option value="saab">Saab</option>
    </optgroup>
    <optgroup label="German Cars">
      <option value="mercedes">Mercedes</option>
      <option value="audi">Audi</option>
    </optgroup>
  </select>
  ```

-  date 选取日、月、年 ；month 选取月和年； week 选取周和年； time 选取时间（小时和分钟）
- `<caption>`是表格的标题

## 2. 其他

- HTML5中增加了两种全新的数据存储方式：WebStorage和WebSQLDatabase。 **WebStorage**可用于临时或永久保存客户端的少量数据，**WebSQLDatabase**是客户端本地化的一套数据库系统，可以将大量的数据保存在客户端，无须与服务器端进行交互，极大地减轻了服务器端的压力。 

# CSS

## 1. 属性

- `text-transform:capitalize`是首字母大写
- `text-transfrom:lowercase`是全部字母为小写
- `text-transfrom:uppercase`是全部字母为大写
- margin-top、padding-top的值是百分比时，是相对最近父级块级元素的 width，相对最近父级块级元素的 width计算的

## 2. 清除浮动

- 给父元素添加 overflow: hidden;
- 在浮动元素下方（父元素内部）添加空 div，并添加样式 clear: both;
- 设置父元素 :after{content: “”;clear: both; display:block;overflow: hidden;}
- 注：CSS3中:代表伪类选择器，::代表伪元素选择器。但是::也可以使用:代替

# JavaScript

## 1. DOM

- 获取select标签内的所有option标签、选中的option标签的序号，并得到选中的标签和它的value和text

```javascript
<body>
  <form>
    <select id="obj">
      <option value="a">1</option>
      <option value="b">2</option>
      <option value="c">3</option>
    </select>
  </form>
  <script>
    let obj = document.querySelector('#obj')
    let fn = function () {
      let index = obj.selectedIndex
      let options = obj.options
      let luckyDog = options[index].value
      console.log(luckyDog);
    }
    fn()
    obj.addEventListener('change',fn)
  </script>
</body>
```

- canvas对象的getGraphics方法可以获取绘图环境
- 继承关系：HTMLDivElement->HTMLElement->Element->Node->EventTarget
- DOM树中总共分为如下几种节点格式：Element类型（元素节点）、Text类型（文本节点）、Comment类型（注释节点）、Document类型（document节点）

## 2. 浏览器的解析渲染过程

- DOM解析：HTML解析器构建DOM树，并行请求CSS、imge、js
- CSS文件下载完成，开始构建CSSOM（CSS树）
- DOM渲染：CCSOM树和DOM树一起生成Render Tree（渲染树）
- 通过布局(Layout)计算出DOM要显示的宽高、位置、颜色
- 最后显示(Painting)，通过显卡把页面画到屏幕上

## 3. DOM树和渲染树的区别

- DOM 树与 HTML 标签一一对应，包括 head 和隐藏元素
- 渲染树不包括 head 和隐藏元素，大段文本的每一个行都是独立节点，每一个节点都有对应的 css 属性

## 4. 重绘repaint和回流（reflow重排）的区别

- 当渲染树中的元素外观（如：颜色）发生改变，不影响布局时，产生**重绘**
- 当渲染树中的元素的布局（如：尺寸、位置、隐藏/状态状态）发生改变时，产生**重排回流**，同时还产生**重绘**
- JS 获取 Layout 属性值（如：offsetLeft、scrollTop、getComputedStyle 等）也会引起回流。因为浏览器需要通过回流计算最新值
- 回流必将引起重绘，而重绘不一定会引起回流
- 触发回流reflow
  - 添加或删除可见的DOM
  - 元素位置改变
  - 元素尺寸改变
  - 内容改变
  - 页面渲染器初始化
  - 浏览器窗口尺寸改变

## 5. 如何最小化repaint和reflow

- 需要要对DOM元素进行复杂的操作时，可以先隐藏(display:"none")，操作完成后再显示
- 需要创建多个 DOM 节点时，使用 DocumentFragment 创建完后一次性的加入 document，或使用字符串拼接方式构建好对应HTML后再使用innerHTML来修改页面
- 缓存 Layout 属性值，如：var left = elem.offsetLeft; 这样，多次使用 left 只产生一次回流
- 避免用 table 布局（table 元素一旦触发回流就会导致 table 里所有的其它元素回流）
- 避免使用 css 表达式(expression)，因为每次调用都会重新计算值（包括加载页面）
- 尽量使用 css 属性简写，如：用 border 代替 border-width, border-style, border-color
- 批量修改元素样式：elem.className 和 elem.style.cssText 代替 elem.style.xxx

## 6.其他

- 设置display:none后的元素会导致浏览器的重排、重绘【涉及到了DOM结构，导致重排、重绘】
- 设置visibility:hidde后的元素只会导致浏览器重绘而不会重排【元素不可见但存在，保留空间，不影响结构】
- 设置元素opacity:0之后，可以触发点击事件【元素不可见但存在，保留空间，不影响结构，可触发事件】
- 设置元素visibility:hidden之后，无法触发点击事件

## 7. 线程

- 浏览器中有不同的线程
  - GUI渲染线程
  - js线程
  - 定时器触发线程setTimeout
  - 浏览器事件线程onclick
  - http异步线程
  - ……
- 在同一个瞬间，只有一个线程起作用，其他线程处于挂起状态。DOM的渲染对应的就是GUI渲染线程；JS的执行对应的就是JS线程；所以，DOM的渲染与JS代码的运行，在同一瞬间只能有一个执行。
- CSS和DOM都属于GUI渲染线程
  - css的加载**不会**阻塞DOM的**解析**
  - css的加载**会**阻塞DOM的**渲染**
- js和DOM属于不同的线程
  - JS的**加载和执行**会阻塞DOM的**解析**
  - JS的**加载和执行**会阻塞DOM的**渲染**

- js和CSS属于不同的线程
  - css加载会阻塞后面js语句的执行

## 8. 事件

- 页面所有资源加载完毕后，会触发 onload 事件

## 9. MVC

- m，model，模型，相当于业务逻辑
- v， view， 视图，相当于网页
- c，controller， 控制器， 相当于页面中的交互