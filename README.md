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
``` 
<?xml version="1.0" standalone="no"?>
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
```

