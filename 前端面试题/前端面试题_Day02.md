# HTML

## 1. 标签

- `<pre>`定义**预格式化的文本**。常见应用是用来表示计算机的源代码，即在pre标签内部用各种转义符号包裹html代码。

- `<q>` 定义**短的引用**，会在内容上添加引号

- `<blockquote`定义**块引用**，会将内容从常规文本中分离出来，左右缩进

- `<embed>`定义**嵌入的内容**

- `<source>` 标签为媒介元素（比如 `<video>` 和 `<audio>`）**定义媒介资源**，允许您规定可替换的视频/音频文件供浏览器根据它对媒体类型或者编解码器的支持进行选择。

- `<track>` 标签为诸如 video 元素之类的媒介**规定外部文本轨道**。用于规定字幕文件或其他包含文本的文件，当媒介播放时，这些文件是可见的。目前主流浏览器都不支持track标签

- `<sup>`标签定义**上标**，`<sub>`标签定义**下标**

- `<meter>` 标签定义已知范围或分数值内的**标量测量**，也被称为 gauge（尺度）。`<meter>` 标签不应用于指示进度（在进度条中）。

-  `<progress>` 标签用于**标记进度条**。

- `<i>`标签表示**斜体**，`<b>`标签表示**加粗**

- 一个常用的针对移动网页优化过的页面的 viewport meta 标签大致如下：

  ```
  <meta name=``"viewport"` `content=``"width=device-width, initial-scale=1.0"``>
  ```

  - width：控制 viewport 的大小，可以指定的一个值，如 600，或者特殊的值，如 device-width 为设备的宽度（单位为缩放为 100% 时的 CSS 的像素）。
  - height：和 width 相对应，指定高度。
  - initial-scale：初始缩放比例，也即是当页面第一次 load 的时候缩放比例。
  - maximum-scale：允许用户缩放到的最大比例。
  - minimum-scale：允许用户缩放到的最小比例。
  - user-scalable：用户是否可以手动缩放。

## 2. 属性

- HTML5中的属性名对**大小写不敏感**，推荐使用小写
- **data-*属性**用于存储页面或应用程序的私有自定义数据，赋予我们在所有 HTML 元素上嵌入自定义 data 属性的能力，存储的（自定义）数据能够被页面的 JavaScript 中利用，创建更好的用户体验。
- **contenteditable属性**用于规定元素内容是否是可编辑的

## 3. 其他

- 浏览器渲染流程
  - 解析HTML并构建DOM树
  - 构建render（渲染）树
  - 布局render（渲染）树
  - 绘制render（渲染）树
- XML, JSON
  - JSON比XML在数据编码上JSON更具有效率，更节约空间，更能表达结构化数据
  - XML对数据的类型描述表达比JSON更丰富
  - 存在一些数据库，直接支持XML或JSON数据的操作，如mongodb, postgresql

## 4. session、cookie

- http是无状态协议，即这一次请求和上一次请求是没有任何关系的。
- 为了使某个域名下的所有网页能够共享某些数据（如登录信息），使用session和cookie
- 客户端访问服务器的流程
  - 客户端 **发送http请求** 服务器端
  - 服务器端接收请求后**建立session，返回响应，其中包含Set-Cookie头部，里面包含sessionId**
  - 客户端二次请求时**携带设置好的cookie**
  - 服务器端接收请求，**分解cookie，验证信息**，核对成功后返回响应
- cookie是实现session的最常用的方案，但不是唯一方案。

## 5. token

- 用户登录的时候，服务端生成一个token（通过登录信息做数字签名，加密之后得到的字符串）返回给客户端
- 客户端后续的请求都带上这个token
- 服务端解析token（做解密和签名认证，判断其有效性）获取用户信息，并响应用户的请求。
- token会有过期时间，客户端登出的时候也会废弃token，但是服务端不需要任何操作

## 6. session和token的区别

- session
  - 为无状态的HTTP提供持久机制。
  - 如果需要实现有状态的会话，可以增加Session来在服务端保存一些状态。
  - 只提供一种简单的认证，数据只保存在站点，不应该共享给其他网站或者第三方APP
- token
  - 就是一个令牌。
  - 作为身份认证安全性更好。
  - 如果你的用户数据可能需要和第三方共享，或者允许第三方调用API接口，用token。
- session 要求服务端存储信息，并根据id能够检索，而 token 不需要。
- 服务端 要 通过 token 来解析 用户身份，也需要定义好相应的协议。
- session 一般使用cookie 来交互。token，可以是 cookie，也可以是 其他heaser，甚至可以放在请求的内容中。不使用cookie可以带来跨域的便利性
- 很多情况下，sessin 和 token 可以一起使用。
- token 技术 对应的标准，就是JWT
- token 完全由应用管理，所以它可以避开同源策略
- token 可以避免 CSRF 攻击(因为不需要 cookie )
- 移动端对 cookie 的支持不是很好，而 session 需要基于 cookie 实现，所以移动端常用的是 token

## 7. sessionStorage、localStorage

- HTML5中的WebStorage包括两种存储方式：sessionStorage、localStorage
- localStorage和sessionStorage一样都是用来存储客户端临时信息的对象，存储大小为5MB，有相同的Web API
- sessionStorage
  - 有期限，当窗口或浏览器关闭时就会被销毁
  - 在同源的不同窗口下不可共享
  - 应用场景：页面传值
- localStorage
  - 无限期，关闭浏览器后仍存在，除非用户手动在浏览器UI层删除
  - 在同源的不同窗口下可共享，在不同浏览器中不可共享
  - 应用场景：适合长期保存在本地的数据，如存储该浏览器对该页面的访问次数

# CSS

## 1. 部分属性

- align属性规定 div 元素中的内容的水平对齐方式

# JavaScript

## 1. DOM

- 事件
  - onchange()会在域的内容改变时发生，也可在单选框与复选框改变后触发。可以使用于： `<input>`,`<select>`和 `<textarea>`。
  - onblur()对象失去焦点；onfocus()对象获得焦点

## 2. 其他

- jQuery方法
  - .fadeIn() 使用淡入效果显示元素
  - .fadeOut() 淡入效果隐藏元素
  - .fadeToggle() 淡入效果显示 / 隐藏元素来回切换
  - .fadeTo() 元素的透明度逐渐变化到制定的值

- 跨域
  - CSS 文件的加载不受跨域限制
  - window.onerror 方法默认情况下无法获取跨域脚本的报错详情
  - canvas 中使用 drawImage 贴图会受跨域限制
  - Web 字体、图片等资源文件加载受浏览器跨域限制
