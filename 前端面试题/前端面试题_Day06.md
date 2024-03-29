# HTML

## 1. 列表

- list列表符号：`list-style-type: square`
- fieldset用来分组，legend用来分组描述
- em表示强调，用斜体显示；strong表示更强的强调，用粗体显示

# CSS

## 1. 选择器优先级

- 最高优先级：内联样式
- 次优先级：id选择器
- 其次优先级：类选择器，伪类选择器
- 最后优先级：标签选择器

## 2. 结构伪类选择器

E:nth-child(n)会将父元素的所有子元素排序，然后核对第n项是否是E标签。如果是则修改样式，否则不予操作。包括n是odd奇数项，even偶数项。括号内的变量n从0开始，括号内的表达式从1开始，表达式值为0时忽略。

E:nth-of-type(n)则会将指定的E标签元素排序，进行修改样式。

如果是无序列表，两者作用相同，多用E:nth-child(n)

## 3. position定位

| 值       | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| absolute | 绝对定位，相对于static定位之外的第一个父元素进行定位 。脱离文档流 |
| fixed    | 固定定位，相对于浏览器窗口进行定位 。脱离文档流              |
| relative | 相对定位，相对于其正常位置进行定位 。不脱离文档流            |
| static   | 没有定位，出现在正常的流中。不脱离文档流                     |
| inherit  | 从父元素继承position属性的值                                 |

## 4. float浮动

- 行内元素与浮动元素发生重叠，边框、背景、内容都会显示在浮动元素之上
- 块级元素与浮动元素发生重叠，边框、背景会显示在浮动元素之下，内容会显示在浮动元素之上
- 若不浮动的是块级元素，那么浮动的元素将显示在其上方
- 若不浮动的是行内元素或者行内块元素，那么浮动的元素不会覆盖它，而是将其挤往左方

## 5. BFC：Block formatting context

- BFC属于普通流，可以看做是隔离的独立容器，容器里面的元素不会在布局上影响到其他的元素。
- 特性：避免外边距重叠；清除浮动；阻止元素被浮动元素覆盖
- 触发BFC
  - html
  - 浮动元素
  - 绝对定位/固定定位元素
  - display不为block，为inline-block, flex, grid等
  - overflow不为visible的块元素
  - contain为layout, content, paint的元素
  - 多列容器

## 6. 其他

- 使超出的文字部分变成...：`text-overflow: ellipsis;`
- 标签显示优先级：帧元素比表单元素优先，表单元素比非表单元素优先
- 运用CSS3动画，需要运用keyframes规则，animation属性
- CSS使用服务端的字体：@font-face
- 预编译CSS工具：Less，Sass，Stylus
- 使用table时，需要设置cellpadding, cellspacing
- background-position的值用百分比表示时，表示背景图像离其容器的距离是这个图宽度/高度的百分比。当只有一个取值时，第二个取值默认50%

## 7. 清除浮动

- 在浮动元素末尾添加一个空的标签例如 `<div style="clear:both"></div>`
  - 优点：简单，代码少，浏览器兼容好
  - 需要添加大量无语义的html元素，不易维护
- 通过设置父元素 overflow 值为 hidden
- 给父元素添加 clearfix 类，这个类是结合::before和::after伪元素
  - ::before伪元素是给其内部的前面加入内容
  - ::after伪元素是给其内部的最后加入内容
- 给浮动元素的父元素也添加浮动
  - 缺点：影响布局，不推荐使用

# JavaScript

