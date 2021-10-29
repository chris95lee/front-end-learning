# HTML

## 1. 元素

- 块级元素：div, p, h1-h6, ul, li, form【可以设置width, height, padding, margin】
- 行内块元素：img, input【可以设置width, height, padding, margin】
- 内联元素：label, span,a, strong, em, del, ins【不可以设置width, height,padding/margin-top/bottom, 可以设置padding/margin-left/right】

## 2. iframe

`<iframe>`标签规定一个内联框架。一个内联框架被用来在当前 HTML 文档中嵌入另一个文档。

使用场景有

- 与第三方域名下的页面共享cookie
- 上传图片，避免当前页刷新
- 左边固定右边自适应的布局
- 资源加载

## 3. 概念

- HTML属性：为 HTML 元素提供附加信息，如a标签的href属性，class, id, title属性
- HTML元素：HTML 元素指的是从开始标签（start tag）到结束标签（end tag）的所有代码
- 事件属性：onload, onfocus等
- 样式属性：font-size, text-align等

# CSS

## 1. 屏幕尺寸

| 超小屏幕（手机） | 小屏幕（平板） | 中等屏幕（桌面） | 大屏幕（桌面） |
| ---------------- | -------------- | ---------------- | -------------- |
| <768px           | >=768px        | >=992px          | >=1200px       |
| .col-xs-         | .col-sm-       | .col-ms-         | .col-lg-       |



# JavaScript

## 1. Window对象

- 浏览器打开HTML文档时，通常会创建一个Window对象
- Window对象表示浏览器的窗口，可用于检索有关窗口状态的信息
- Window对象是浏览器所有内容的主容器
- 如果文档包含框架（`<frame>` 或 `<iframe>` 标签），浏览器会为 HTML 文档创建一个 window 对象，并为每个框架创建一个额外的 window 对象。

## 2. 优化滚动性能

- 在滚动中对滚动函数进行节流处理
- 对滚动事件进行防抖处理
- 滚动中减少导致重绘的操作
- 滚动中减少导致重排的操作

## 3. 带有id属性的DOM元素

- 如果一个元素拥有属性，那么window对象里会创建一个全局变量，变量名就是这个元素的id属性值
- 这样会增加内存负担

