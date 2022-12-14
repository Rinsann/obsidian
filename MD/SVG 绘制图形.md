## 引言

`SVG` 是 `XML` 语言的一种形式，有点类似 `XHTML` ，它可以用来绘制矢量图形。`SVG` 可以通过定义必要的线和形状来创建一个图形，也可以修改已有的位图，或者将这两种方式结合起来创建图形。图形和其组成部分可以变形，可以合成，还可以通过滤镜完全改变外观。

`SVG` 推出于 1999 年，之前有几个相互竞争的格式规范被提交到 `W3C`，但是都没有完全通过。当下的浏览器支持程度请参考[Can I use](https://caniuse.com/)。即便浏览器实现了一些规范，但实现速度完全不能和它的竞争技术相比，它的竞争技术比如说`HTML Canvas和Adobe Flash`，都已经实现了成熟的应用接口。但是 `SVG` 也有自身的优点，比如它实现了 `DOM` 接口（比 `Canvas` 方便），不需要安装第三方插件就可以在浏览器中使用（比 `Flash` 方便）。当然，是否使用 `SVG` 还要取决于你要实现什么

`SVG` 与 `Flash` 类似，都是用于二维矢量图形，二者的区别在于，`SVG` 是一个 `W3C` 标准，基于 `XML`，是开放的，而 `Flash` 是封闭的基于二进制格式的。因为都是 `W3C` 标准，`SVG` 与其他的 `W3C` 标准，比如 `CSS`、`DOM` 和 `SMIL` 等能够协同工作。

`SVG` 与 `Canvas` 也类似，都是用于绘制图形，区别在于 `Canvas` 是非矢量的，而 `SVG` 是矢量的（放大不模糊），并且 `SVG` 比 `Canvas` 有更丰富的效果。

## 基本要素

`HTML` 提供了定义标题、段落、表格等等内容的元素。与此类似，`SVG` 也提供了一些元素，用于定义圆形、矩形、简单或复杂的曲线，以及其他形状。一个简单的 `SVG` 文档由`<svg>`根元素和基本的形状元素构成。另外还有一个 `g` 元素，它用来把若干个基本形状编成一个组。

从这些开始，`SVG` 可以成为任何复杂的组合图形。`SVG` 支持渐变、旋转、滤镜效果、`JavaScript`接口等等功能，但是所有这些额外的语言特性，都需要在一个定义好的图形区域内实现。

## 注意事项

正式开始之前，你需要基本掌握 `XML` 和其它标记语言比如说 `HTML`，如果你不是很熟悉 `XML`，这里有几个重点一定要记住：

-   `SVG` 的元素和属性必须按标准格式书写，因为 `XML` 是区分大小写的（这一点和 `html` 不同）
-   `SVG` 里的属性值必须用引号引起来，就算是数值也必须这样做。

## SVG的发展

自从 200 3年成为 `W3C` 推荐标准以来，最接近的“完整版” `SVG` 版本是1.1版，它基于1.0版，并且增加了更多便于实现的模块化内容，`SVG1.1` 的第二个版本在2011年成为推荐标准，完整的`SVG1.2` 本来是下一个标准版本，但它又被`SVG2.0`取代。`SVG2.0` 正在制定当中，它采用了类似 `CSS3` 的制定方法，通过若干松散耦合的组件形成一套标准。

除了完整的 `SVG` 推荐标准，`W3C` 工作组还在2003年推出了 `SVG Tiny` 和 `SVG Basic`。这两个配置文件主要瞄准移动设备。首先`SVG Tiny`主要是为性能低的小设备生成图元，而`SVG Basic`实现了完整版 `SVG` 里的很多功能，只是舍弃了难以实现的大型渲染（比如动画）。2008年，`SVG Tiny1.2`成为`W3C`推荐标准。