## 简单范例

让我们直接从一个简单的例子开始，看一下下面代码：

```xml
<svg version="1.1"
     baseProfile="full"
     width="300" height="200"
     xmlns="http://www.w3.org/2000/svg">

  <rect width="100%" height="100%" fill="red" />

  <circle cx="150" cy="100" r="80" fill="green" />

  <text x="150" y="125" font-size="60" text-anchor="middle" fill="white">饥人谷</text>

</svg>
```

复制并粘贴代码到文件 `demo1.svg`。然后用浏览器打开该文件，会看到如下效果。你也可以把代码拷贝到一个 `html` 的 `body` 里，同样会看到效果

![](https://jirengu.github.io/svg-you-should-know/zh-cn/cloud.hunger-valley.com/18-10-8/68976609.jpg)

绘制流程包括以下几步：

1.  从 `svg` 根元素开始：
    -   应舍弃来自 `(X)HTML`的 `doctype` 声明，因为基于 `SVG` 的 `DTD` 验证导致的问题比它能解决的问题更多。
    -   属性 `version` 和属性 `baseProfile` 属性是必不可少的，供其它类型的验证方式确定SVG版本。
    -   作为 `XML` 的一种方言，`SVG` 必须正确的绑定命名空间 （在 `xmlns` 属性中绑定）。 请阅读命名空间速成 页面获取更多信息。
2.  绘制一个完全覆盖图像区域的矩形 `<rect/>`，把背景颜色设为红色。
3.  一个半径 `80px` 的绿色圆圈`<circle/>`绘制在红色矩形的正中央 （向右偏移`150px`，向下偏移`100px`）。
4.  绘制文字“`SVG`”。文字被填充为白色， 通过设置居中的锚点把文字定位到期望的位置：在这种情况下，中心点应该对应于绿色圆圈的中点。还可以精细调整字体大小和垂直位置，确保最后的样式是美观的。

## SVG 的使用

有几种使用 `SVG` 的方式

### 直接嵌入到 `HTML` 中

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
</head>
<body>
  <svg version="1.1" width="300" height="200">
    <rect width="100%" height="100%" fill="red" />
    <circle cx="150" cy="100" r="80" fill="green" />
    <text x="150" y="125" font-size="60" text-anchor="middle" fill="white">饥人谷</text>
  </svg>
</body>
</html>
```

### `img` 标签引入 `svg` 文件

```html
<img src="logo.svg">
```

### `CSS` 背景图片引入

```css
.logo {
  background: url(logo.svg)
}
```

### `object` 元素引入 `svg` 文件

```html
<object data="image.svg" type="image/svg+xml" />
```

### `iframe` 元素引用 `SVG` 文件

不建议使用

```html
<iframe src="image.svg"></iframe>
```

## 坐标定位

`SVG` 坐标系统是：以页面的左上角为`(0,0)`坐标点，坐标以像素为单位，`x` 轴正方向是向右，`y` 轴正方向是向下。注意，这和你小时候所教的绘图方式是相反的。但是在 `HTML` 文档中，元素都是用这种方式定位的。

![](https://cloud.hunger-valley.com/18-10-8/75302148.jpg)

示例：

```xml
<rect x="0" y="0" width="100" height="100" />
```

定义一个矩形，即从左上角开始，向右延展 `100px`，向下延展 `100px`，形成一个`100*100`大的矩形。

### 像素

在没有进一步规范说明的情况下，1单位等同于1个屏幕单位。要明确改变这种设定，`SVG` 里有多种方法。我们从 `svg` 根元素开始：

```xml
<svg width="100" height="100">
```

上面的元素定义了一个`100*100px`的SVG画布，这里1单位等同于1屏幕单位。

```xml
<svg width="200" height="200" viewBox="0 0 100 100">
```

这里定义的画布尺寸是`200*200px`。但是，`viewBox` 属性定义了画布上可以显示的区域：从(0,0)点开始，`100宽*100高` 的区域。这个 `100*100` 的区域，会放到 `200*200` 的画布上显示。于是就形成了放大两倍的效果。


## 基本形状

要想插入一个形状，你可以在文档中创建一个元素。不同的元素对应着不同的形状，并且使用不同的属性来定义图形的大小和位置

```xml
<?xml version="1.0" standalone="no"?
<svg width="200" height="250" version="1.1" xmlns="http://www.w3.org/2000/svg">

  <rect x="10" y="10" width="30" height="30" stroke="black" fill="transparent" stroke-width="5"/>
  <rect x="60" y="10" rx="10" ry="10" width="30" height="30" stroke="black" fill="transparent" stroke-width="5"/>

  <circle cx="25" cy="75" r="20" stroke="red" fill="transparent" stroke-width="5"/>
  <ellipse cx="75" cy="75" rx="20" ry="5" stroke="red" fill="transparent" stroke-width="5"/>

  <line x1="10" x2="50" y1="110" y2="150" stroke="orange" fill="transparent" stroke-width="5"/>
  <polyline points="60 110 65 120 70 115 75 130 80 125 85 140 90 135 95 150 100 145"
      stroke="orange" fill="transparent" stroke-width="5"/>

  <polygon points="50 160 55 180 70 180 60 190 65 205 50 195 35 205 40 190 30 180 45 180"
      stroke="green" fill="transparent" stroke-width="5"/>

  <path d="M20,230 Q40,205 50,230 T90,230" fill="none" stroke="blue" stroke-width="5"/>
</svg>
```

### 矩形

`rect` 元素会在屏幕上绘制一个矩形 。其实只要6个基本属性就可以控制它在屏幕上的位置和形状。`rx` 和 `ry` 属性用来控制圆角。如果没有设置圆角，则默认为0。

```xml
<rect x="10" y="10" width="30" height="30"/>
<rect x="60" y="10" rx="10" ry="10" width="30" height="30"/>
```

-   `x`
    -   矩形左上角的 `x` 位置
-   `y`
    -   矩形左上角的 `y` 位置
-   `width`
    -   矩形的宽度
-   `height`
    -   矩形的高度
-   `rx`
    -   圆角的 `x` 方位的半径
-   `ry`
    -   圆角的 `y` 方位的半径

### 圆形

`circle` 元素会在屏幕上绘制一个圆形。它只有 `3` 个属性用来设置圆形。

```xml
<circle cx="25" cy="75" r="20"/>
```

-   `r`
    -   圆的半径
-   `cx`
    -   圆心的 `x` 位置
-   `cy`
    -   圆心的 `y` 位置

### 椭圆

`Ellipse` 是 `circle` 元素更通用的形式，你可以分别缩放圆的 `x` 半径和 `y` 半径（长轴半径和短轴半径）。

```xml
<ellipse cx="75" cy="75" rx="20" ry="5"/>
```

-   `rx`
    -   椭圆的 `x` 半径
-   `ry`
    -   椭圆的 `y` 半径
-   `cx`
    -   椭圆中心的 `x` 位置
-   `cy`
    -   椭圆中心的 `y` 位置

### 直线

`Line` 绘制直线。它取两个点的位置作为属性，指定这条线的起点和终点位置。

```xml
<line x1="10" x2="50" y1="110" y2="150"/>
```

-   `x1`
    -   起点的 `x` 位置
-   `y1`
    -   起点的 `y` 位置
-   `x2`
    -   终点的 `x` 位置
-   `y2`
    -   终点的 `y` 位置

### 折线

`Polyline` 是一组连接在一起的直线。因为它可以有很多的点，折线的的所有点位置都放在一个`points` 属性中：

```xml
<polyline points="60 110, 65 120, 70 115, 75 130, 80 125, 85 140, 90 135, 95 150, 100 145"/>
```

-   `points`
    -   点集数列。每个数字用空白、逗号、终止命令符或者换行符分隔开。每个点必须包含2个数字，一个是 `x` 坐标，一个是 `y` 坐标。所以点列表 (0,0), (1,1) 和(2,2)可以写成这样：`0 0, 1 1, 2 2`。

### 多边形

`polygon` 和折线很像，它们都是由连接一组点集的直线构成。不同的是，`polygon` 的路径在最后一个点处自动回到第一个点。需要注意的是，矩形也是一种多边形，如果需要更多灵活性的话，你也可以用多边形创建一个矩形。

```xml
<polygon points="50 160, 55 180, 70 180, 60 190, 65 205, 50 195, 35 205, 40 190, 30 180, 45 180"/>
```

-   `points`
    -   点集数列。每个数字用空白符、逗号、终止命令或者换行符分隔开。每个点必须包含2个数字，一个是 `x` 坐标，一个是 `y` 坐标。所以点列表 (0,0), (1,1) 和(2,2)可以写成这样：`0 0, 1 1, 2 2`。路径绘制完后闭合图形，所以最终的直线将从位置(2,2)连接到位置(0,0)。

## 路径

`path` 可能是 `SVG` 中最常见的形状。你可以用 `path` 元素绘制矩形（直角矩形或者圆角矩形）、圆形、椭圆、折线形、多边形，以及一些其他的形状，例如贝塞尔曲线、2次曲线等曲线。因为 `path` 很强大也很复杂，先试试定义一个路径形状的属性。

```xml
<path d="M 20 230 Q 40 205, 50 230 T 90230"/>
```

-   `d`
    -   一个点集数列以及其它关于如何绘制路径的信息