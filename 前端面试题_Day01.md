# HTML

## 1. `<main>`一般包括什么

- !doctype
- html
  - head
  - body
    - header
    - main
    - slider
    - footer

## 2. DOCTYPE的声明

文档类型 DOCTYPE 的声明是必要的。

HTML 5的文档头部，都要声明"<!DOCTYPE html>" 

HTML 4.01和XHTML 1.0在声明时需要引用DTD（strict, transitional, frameset)

标准（严格）模式：指浏览器按照W3C标准解析执行代码

混杂（怪异）模式：浏览器以一种比较宽松的向后兼容的自己的方式解析执行代码

- 不存在DOCTYPE
- 有transitional/ frameset DTD 但没有URI
- 盒子模型、!important、行内元素的高宽、margin:0 auto等在标准模型和怪异模型中有不同

dcotype的声明不限于“<!DOCTYPE html>" 确保浏览器按照最佳的相关规范进行渲染，而不是使用“怪异模式”的渲染模式。


## 4. DHTML

三个主要优点：

- 动态样式（使网页作者改变内容的外部特征而不强制用户再次下载全部内容）
- 动态内容
- 动态定位

## 5. SVG

什么是SVG? 

- SVG 指可伸缩矢量图形 (Scalable Vector Graphics)
- SVG 用来定义用于网络的基于矢量的图形
- SVG 使用 XML 格式定义图形
- SVG 图像在放大或改变尺寸的情况下其图形质量不会有所损失
- SVG 是万维网联盟的标准
- SVG 与诸如 DOM 和 XSL 之类的 W3C 标准是一个整体
- SVG是HTML下的一个分支

## 6. canvas

- canvas是HTML5的一部分，允许脚本动态渲染位图
- canvas拥有多种绘制路径、矩形、圆形、字符及添加图像的方法
- Internet Explorer自Internet Explorer9起已经可以支持canvas
- canvas中绘制的元素不可以通过浏览器提供的接口获取到
- HTML5（不是canvas）作为Flash的替代技术出现【B站播放器html5和flash】

# CSS

## 1. 选择器

- .a，.b｛“,”**逗号**指相同的css样式｝

- .a .b｛“ ”**空格**指后代元素｝

- .a>.b｛“>”指子代所有元素｝

- .a + .b｛“+”指选择相邻兄弟，叫做“相邻兄弟选择器”

  例：h1 + p {margin-top:50px;}这个选择器读作：“选择紧接在 h1 元素后出现的段落，h1 和 p 元素拥有共同的父元素”。｝

- ul>li:nth-child(3n+1) 这里的n是从0开始计数。得到的3n+1可以代表第一个li，而不是0来代表第一个li



## 2. clientWidth、offsetWidth等属性

ele.clientWidth = 宽度 + padding

ele.offsetWidth = 宽度 + padding + border

# JavaScript

## 1. DOM操作效率

- 处理列表子元素的点击事件时，使用事件代理  // 事件代理是根据事件冒泡原理，使用事件代理可以减少注册事件,节省内存【可以提高效率】
- 插入大量DOM元素时，使用innerHTML替代逐个构建元素 // 测试后发现innerHTML比creaetElement效率要高【可以提高效率】
- 使用DocumentFragment替代多次appendChild操作 // 将元素放入代码片段中一次插入比你创建一个插入一个效率肯定要高的多【可以提高效率】
- 使用addEventListener替代 onxxx(比如onclick) 进行事件绑定 // 使用addEventListener监听事件不会被覆盖，而on会覆盖上一个事件【不可以提高效率】

