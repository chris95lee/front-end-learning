# HTML

## 1. 使用form元素的属性enctype

enctype 属性规定在发送到服务器之前应该如何对表单数据进行编码。

属性值

application/x-www-form-urlencoded 
在发送前编码所有字符（默认） 

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

## 3. 其他

- 网页中，rem 作为元素尺寸单位时，是相对 文档根节点的 font-size 进行计算的。
- 目前最新的 Microsoft Internet Explorer 中，盒模型默认使用的是 content-box。怪异模式下使用的是border-box

# JavaScript