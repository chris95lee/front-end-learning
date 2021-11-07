# HTML

## 1. 使用form元素的属性enctype

enctype 属性规定在发送到服务器之前应该如何对表单数据进行编码。

属性值:

application/x-www-form-urlencoded 
在发送前编码所有字符**（默认）** 

multipart/form-data 
不对字符编码。 在使用包含文件上传控件的表单时，必须使用该值。

text/plain 
空格转换为 "+" 加号，但不对特殊字符编码。

## 2. fieldset和legend

```html
<form action="#" method="post">
    <fieldset>
      <legend>老婆</legend>
      蒙德：<input type="text"><br />
      璃月：<input type="text"><br />
      稻妻：<input type="text"><br />
    </fieldset>
    <fieldset>
      <legend>老公</legend>
      蒙德：<input type="text"><br />
      璃月：<input type="text"><br />
      稻妻：<input type="text"><br />
    </fieldset>
  </form>
```

## 3. 跨文档消息传输

跨文档消息传送（cross-document messaging），简称XDM，指的是来自不同域的页面间传递消息。
XDM的核心是postMessage()方法。目的：向另一个地方传递数据。对于XDM而言，“另一个地方”指的是包含在当前页面中的<iframe>元素，或者由当前页面弹出的窗口。
postMessage()方法接收两个参数：一条消息和一个表示消息接收方来自哪个域的字符串。第二个参数对保障安全通信非常重要，可以防止浏览器把消息发送到不安全的地方。
接收到XDM消息时，会触发window对象的message事件。这个事件是以异步形式触发的，因此从发送消息到接受消息（触发接受窗口的message事件）可能要经过一段时间的延迟。
有了XDM，包含<iframe>的页面可以确保自身不受恶意内容的侵扰，因为它只通过XDM为嵌入的框架通信。而XDM也可以来自相同域的页面间使用。

## 4. 多媒体标签Audio/Video

| 方法           | 描述                                    |
| -------------- | --------------------------------------- |
| addTextTrack() | 添加文本轨道                            |
| canPlayType()  | 检测浏览器是否能播放指定的音频/视频类型 |
| load()         | 重新加载                                |
| play()         | 开始播放                                |
| pause()        | 暂停播放                                |

`<audio>`可以在开始标签和结束标签之间放置文本内容，这样老的浏览器就可以显示出不支持该标签的信息

事件：play() playing() pause() seeked() seeking() abort()当音频/视频的加载已放弃时触发

## 5. WEB应用特有的作用域

会话作用域、请求作用域、应用上下文

## 6. 标签

HTML5 规范声明：应该使用 `<h1> - <h6>` 来表示标题，使用 `<em>` 标签来表示强调的文本，应该使用 `<strong>` 标签来表示重要文本，应该使用 `<mark>` 标签来表示标注的/突出显示的文本，在没有其他合适标签更合适时，才应该把 `<b>` 标签作为最后的选项。

`<h1> - <h6>` 标签表示 HTML 标题，默认加粗

`<caption>` 标签表示表格标题，标题一般被居中表格之上，但不加粗文本

`<em>` 标签表示强调内容，显示为斜体，但不加粗文本

`<th>` 标签表示表格的表头，默认加粗文本

`<manifest>`标签用于应用缓存资源清单

p是块元素，但是其不能包含除了它本身之外的任何块元素；

a是内联元素，但是它可以包含除了它本身外的任意块元素。

## 7. form表单中input元素的readonly和disabled属性

disabled和readonly这两个属性有一些共同之处，比如都设为true，则form属性将不能被编辑，往往在写[js](http://lib.csdn.net/base/javascript)代码的时候容易混合使用这两个属性，其实他们之间是有一定区别的：

- 如果一个输入项的disabled设为true，则该表单输入项**不能获取焦点**，用户的所有操作（鼠标点击和键盘输入等）对该输入项都无效，最重要的一点是当提交表单时，这个表单输入项将**不会被提交**。
- 而readonly只是针对文本输入框这类可以输入文本的输入项，如果设为true，用户只是**不能编辑对应的文本，但是仍然可以聚焦焦点**，并且在提交表单的时候，该输入项会**作为form的一项提交**。

# CSS

## 1. a标签的锚伪类

在支持 css 的浏览器中，链接的不同状态都可以不同的方式显示，这些状态包括：活动状态，已被访问状态，未被访问状态和鼠标悬停状态。用来表示链接不同状态的伪类就是锚伪类。

```css
<style>
    body {color: grey;}
    a {color: red;}
	/*定义时必须保持lvha顺序：link-visited-hover-active*/
	a:link {color: green;} /* 未访问的链接 */
    a:visited {color: blue;} /* 已访问的链接 */
    a:hover {color:orange;} /* 鼠标移动到链接上 */
    a:active {color: yellow;} /* 选定的链接 */
</style>
```

## 2. 定位

- 当元素的 position 属性设置为 relative 时，设置的 top、right、bottom、left 偏移值是相对于其自身的。
- 当元素的 position 属性设置为 absolute 时，设置的 top、right、bottom、left 偏移值是相对于其上一级有定位的祖先元素。

## 3. 引入CSS

```html
<link rel="stylesheet" type="text/css" href="test.css">
<style type=”text/css”>body{color:red}</style>
@import
```

- link
  - link 属于 XHTML 标签，无兼容问题，除了加载 CSS 外，还能用于定义 RSS，定义 rel 连接属性等作用；
  - link标签是同时加载的；link的加载和解析是两个概念，加载是并行的，解析是顺序的
  - link 引用 CSS 时，页面加载同时加载样式；
  - link 支持使用 JS 控制 DOM 去改变样式

- @import
  - @import 是 CSS 提供的，只能用于加载 CSS	
  - @import 需要页面完全加载完再加载
  - @import 不支持js控制DOM改变样式

（script标签加载完一个再加载另一个）



## 4. 其他

- 网页中，rem 作为元素尺寸单位时，是相对 文档根节点的 font-size 进行计算的。
- 目前最新的 Microsoft Internet Explorer 中，盒模型默认使用的是 content-box。怪异模式下使用的是border-box

## 5. BFC

BFC(Block formatting context)直译为"块级格式化上下文"。它是一个独立的渲染区域，只有Block-level box参与,

哪些情况会产生BFC:

1. 根元素
2. float属性不为none
3. position为absolute或fixed
4. display为inline-block, table-cell, table-caption, flex, inline-flex
5. overflow不为visible

## 6. 继承

**一、无继承性的属性**

1、display：规定元素应该生成的框的类型

2、文本属性：

vertical-align：垂直文本对齐

text-decoration：规定添加到文本的装饰

text-shadow：文本阴影效果

white-space：空白符的处理

unicode-bidi：设置文本的方向

3、盒子模型的属性：width、height、margin 、margin-top、margin-right、margin-bottom、margin-left、border、border-style、border-top-style、border-right-style、border-bottom-style、border-left-style、border-width、border-top-width、border-right-right、border-bottom-width、border-left-width、border-color、border-top-color、border-right-color、border-bottom-color、border-left-color、border-top、border-right、border-bottom、border-left、padding、padding-top、padding-right、padding-bottom、padding-left

4、背景属性：background、background-color、background-image、background-repeat、background-position、background-attachment

5、定位属性：float、clear、position、top、right、bottom、left、min-width、min-height、max-width、max-height、overflow、clip、z-index

6、生成内容属性：content、counter-reset、counter-increment

7、轮廓样式属性：outline-style、outline-width、outline-color、outline

8、页面样式属性：size、page-break-before、page-break-after

9、声音样式属性：pause-before、pause-after、pause、cue-before、cue-after、cue、play-during

 **二、有继承性的属性**

1、字体系列属性

font：组合字体

font-family：规定元素的字体系列

font-weight：设置字体的粗细

font-size：设置字体的尺寸

font-style：定义字体的风格

font-variant：设置小型大写字母的字体显示文本，这意味着所有的小写字母均会被转换为大写，但是所有使用小型大写字体的字母与其余文本相比，其字体尺寸更小。

font-stretch：对当前的 font-family 进行伸缩变形。所有主流浏览器都不支持。

font-size-adjust：为某个元素规定一个 aspect 值，这样就可以保持首选字体的 x-height。

2、文本系列属性

text-indent：文本缩进

text-align：文本水平对齐

line-height：行高

word-spacing：增加或减少单词间的空白（即字间隔）

letter-spacing：增加或减少字符间的空白（字符间距）

text-transform：控制文本大小写

direction：规定文本的书写方向

color：文本颜色

3、元素可见性：visibility

4、表格布局属性：caption-side、border-collapse、border-spacing、empty-cells、table-layout

5、列表布局属性：list-style-type、list-style-image、list-style-position、list-style

6、生成内容属性：quotes

7、光标属性：cursor

8、页面样式属性：page、page-break-inside、windows、orphans

9、声音样式属性：speak、speak-punctuation、speak-numeral、speak-header、speech-rate、volume、voice-family、pitch、pitch-range、stress、richness、、azimuth、elevation

 三、**所有元素可以继承的属性**

1、元素可见性：visibility

2、光标属性：cursor

 四、**内联元素可以继承的属性**

1、字体系列属性

2、除text-indent、text-align之外的文本系列属性

 五、**块级元素可以继承的属性**

1、text-indent、text-align

# JavaScript

