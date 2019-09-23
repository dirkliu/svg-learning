# SVG学习
SVG是XML语言的一种形式，可以用来绘制矢量图形(https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial/Introduction)

### 基本形状 
https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial/Basic_Shapes 
* 矩形(rect) 
rx: 圆角的x方位的半径  
ry: 圆角的y方位的半径 
``` 
<rect x="10" y="10" width="30" height="30"/> 
<rect x="60" y="10" rx="10" ry="10" width="30" height="30"/>
```
* 圆形(circle)  
r: 圆的半径  
cx: 圆心的x位置  
cy: 圆心的y位置
``` 
<circle cx="25" cy="75" r="20"/>
```
* 椭圆(ellipse)  
rx: 椭圆的x半径  
ry: 椭圆的y半径  
cx: 椭圆中心的x位置  
cy: 椭圆中心的y位置  
``` 
<ellipse cx="75" cy="75" rx="20" ry="5"/>
```
* 线条(line)  
``` 
<line x1="10" x2="50" y1="110" y2="150"/>
```
* 折线(polyline)  
points: 点集数列  
``` 
<polyline points="60 110, 65 120, 70 115, 75 130, 80 125, 85 140, 90 135, 95 150, 100 145"/>
```
* 多边形(polygon)  
``` 
<polygon points="50 160, 55 180, 70 180, 60 190, 65 205, 50 195, 35 205, 40 190, 30 180, 45 180"/>
```
* 路径(path)  
d: 一个点集数列以及其它关于如何绘制路径的信息  
``` 
<path d="M 20 230 Q 40 205, 50 230 T 90230"/>
```

### 路径  
<path>元素是SVG基本形状中最强大的一个。  你可以用它创建线条, 曲线, 弧形等等。https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial/Paths  
* 直线指令  
M x y移动至某个点，不划线；  
L x y移动至新位置并划线;  
H x绘制水平线  
V y绘制垂直线  
* 贝塞尔曲线  
``` 
C x1 y1, x2 y2, x y (or c dx1 dy1, dx2 dy2, dx dy)
```
最后一个坐标(x,y)表示的是曲线的终点，另外两个坐标是控制点，(x1,y1)是起点的控制点，(x2,y2)是终点的控制点。
``` 
S x2 y2, x y (or s dx2 dy2, dx dy)
```
如果S命令跟在一个C或S命令后面，则它的第一个控制点会被假设成前一个命令曲线的第二个控制点的中心对称点。如果S命令单独使用，前面没有C或S命令，那当前点将作为第一个控制点。
``` 
Q x1 y1, x y (or q dx1 dy1, dx dy)
``` 
二次贝塞尔曲线Q，它比三次贝塞尔曲线简单，只需要一个控制点，用来确定起点和终点的曲线斜率。因此它需要两组参数，控制点和终点坐标。
``` 
T x y (or t dx dy)
```
令T会通过前一个控制点，推断出一个新的控制点。这意味着，在你的第一个控制点后面，可以只定义终点，就创建出一个相当复杂的曲线
* 弧形  
弧形可以视为圆形或椭圆形的一部分  
``` 
A rx ry x-axis-rotation large-arc-flag sweep-flag x y
a rx ry x-axis-rotation large-arc-flag sweep-flag dx dy
```  
rx x轴半径 
ry y轴半径  
x-axis-rotation x轴旋转角度  
large-arc-flag 弧度是否大于180度，0表示小角度弧， 1表示大角弧度  

### 填充和边框  
#### Fill 和 Stroke 属性  
* 上色
fill属性设置对象内部的颜色;  
stroke属性设置绘制对象的线条的颜色;  
* 描边  
stroke-width， stroke-linecap， stroke-linejoin， stroke-dasharray等  

#### 使用CSS
* 利用style属性插入到元素的行间  
``` 
<rect x="10" height="180" y="10" width="180" style="stroke: black; fill: red;"/>
```   
* 利用<style>设置一段样式段落。就像在html里这样的<style>一般放在<head>里，在svg里<style>则放在<defs>标签里  
<pre>
<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg" version="1.1">
  <defs>
    <style type="text/css"><![CDATA[
       #MyRect {
         stroke: black;
         fill: red;
       }
    ]]></style>
  </defs>
  <rect x="10" height="180" y="10" width="180" id="MyRect"/>
</svg>
</pre>

### 渐变 
#### 线性渐变(linearGradient)  
要插入一个线性渐变，你需要在SVG文件的defs元素内部，创建一个<linearGradient> 节点  
``` 
<svg width="120" height="240" version="1.1" xmlns="http://www.w3.org/2000/svg">
  <defs>
      <linearGradient id="Gradient1">
        <stop class="stop1" offset="0%"/>
        <stop class="stop2" offset="50%"/>
        <stop class="stop3" offset="100%"/>
      </linearGradient>
      <linearGradient id="Gradient2" x1="0" x2="0" y1="0" y2="1">
        <stop offset="0%" stop-color="red"/>
        <stop offset="50%" stop-color="black" stop-opacity="0"/>
        <stop offset="100%" stop-color="blue"/>
      </linearGradient>
      <style type="text/css"><![CDATA[
        #rect1 { fill: url(#Gradient1); }
        .stop1 { stop-color: red; }
        .stop2 { stop-color: black; stop-opacity: 0; }
        .stop3 { stop-color: blue; }
      ]]></style>
  </defs>
 
  <rect id="rect1" x="10" y="10" rx="15" ry="15" width="100" height="100"/>
  <rect x="10" y="120" rx="15" ry="15" width="100" height="100" fill="url(#Gradient2)"/>
  
</svg>
```
#### 径向渐变  radialGradient  
从一个点开始发散绘制渐变。创建径向渐变需要在文档的defs中添加一个<radialGradient>元素
``` 
<radialGradient id="Gradient" cx="60" cy="60" r="50" fx="35" fy="35" gradientUnits="userSpaceOnUse">
```

### 图案
<pattern>需要放在SVG文档的<defs>内部  
patternUnits: 用于描述我们使用的属性单元。  
patternContentUnits: 描述了pattern元素基于基本形状使用的单元系统，这个属性默认值为userSpaceOnUse，与patternUnits属性相反，这意味着除非你至少指定其中一个属性值（patternContentUnits或patternUnits），否则在pattern中绘制的形状将与pattern元素使用的坐标系不同，当你手写这部分时会容易混淆。  
``` 
<pattern id="Pattern" width=".25" height=".25" patternContentUnits="objectBoundingBox">
  <rect x="0" y="0" width=".25" height=".25" fill="skyblue"/>
  <rect x="0" y="0" width=".125" height=".125" fill="url(#Gradient2)"/>
  <circle cx=".125" cy=".125" r=".1" fill="url(#Gradient1)" fill-opacity="0.5"/>
</pattern>
```

### Texts 
在SVG中有两种截然不同的文本模式. 一种是写在图像中的文本，另一种是SVG字体。 
``` 
<path id="my_path" d="M 20,20 C 40,40 80,40 100,20" />
<text>
  <textPath xlink:href="#my_path">This text follows a curve.</textPath>
</text>
```  

### 基础变形 
<g>: 利用这个助手，你可以把属性赋给一整个元素集合
``` 
<rect x="20" y="20" width="20" height="20" transform="rotate(45)" />
```

### 剪切与遮罩  
Clipping用来移除在别处定义的元素的部分内容。在这里，任何半透明效果都是不行的。它只能要么显示要么不显示。   
Masking允许使用透明度和灰度值遮罩计算得的软边缘。
#### 剪切： clip  
``` 
<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
  <defs>
    <clipPath id="cut-off-bottom">
      <rect x="0" y="0" width="200" height="100" />
    </clipPath>
  </defs>
  <circle cx="100" cy="100" r="100" clip-path="url(#cut-off-bottom)" />
</svg>
``` 
#### 遮罩： mask  
``` 
<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
  <defs>
    <linearGradient id="Gradient">
      <stop offset="0" stop-color="white" stop-opacity="0" />
      <stop offset="1" stop-color="white" stop-opacity="1" />
    </linearGradient>
    <mask id="Mask">
      <rect x="0" y="0" width="200" height="200" fill="url(#Gradient)"  />
    </mask>
  </defs>
  <rect x="0" y="0" width="200" height="200" fill="green" />
  <rect x="0" y="0" width="200" height="200" fill="red" mask="url(#Mask)" />
</svg>
```  
#### 用opacity定义透明度  
填充和描边还有两个属性是fill-opacity和stroke-opacity，分别用来控制填充和描边的不透明度。需要注意的是描边将绘制在填充的上面。因此，如果你在一个元素上设置了描边透明度，但它同时设有填充，则描边的一半应用填充色，另一半将应用背景色。  
``` 
<svg  width="200" height="200" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" >
  <rect x="0" y="0" width="200" height="200" fill="blue" />
  <circle cx="100" cy="100" r="50" stroke="yellow" stroke-width="40" stroke-opacity=".5" fill="red" />
</svg>
``` 


---
#### links
[SVG文档](https://developer.mozilla.org/zh-CN/docs/Web/SVG)  
[SVG教程](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Tutorial)  


