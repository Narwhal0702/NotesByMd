## 关于canvas绘图

与img标签相比没有src和alt属性，实际上只有height和width两个属性。该元素创造了一个固定大小的画布用来绘制和处理要显示的内容

案例：

```html
<html>
 <head>
  <script type="application/javascript">
    function draw() {
      var canvas = document.getElementById("canvas");
      if (canvas.getContext) {
        var ctx = canvas.getContext("2d");

        ctx.fillStyle = "rgb(200,0,0)";
        ctx.fillRect (10, 10, 55, 50);

        ctx.fillStyle = "rgba(0, 0, 200, 0.5)";
        ctx.fillRect (30, 30, 55, 50);
      }
    }
  </script>
 </head>
 <body onload="draw();">
   <canvas id="canvas" width="150" height="150"></canvas>
 </body>
</html>
```

### 栅格

canvas元素默认被网格所覆盖，通常来说网格中的一个单元相当于canvas元素的一像素，栅格的起点为左上角，所有元素位置相对于原点定位

### 绘制基本图形

* 矩形绘制
  * fillRect(x,y,width,height)：绘制一个填充的矩形
  * strokeRect(x,y,width,height)：绘制一个矩形的边框
  * clearRect()：清除指定的矩形区域，让清除部分完全透明
* 绘制路径
  * beginPath()：新建一条路径，生成之后图形绘制命令被指向到路径上生成路径
  * stroke()：通过线条来绘制图形轮廓
  * fill()：通过填充路径的内容区域生成实心的图形

```js
function draw() {
  var canvas = document.getElementById('canvas');
  if (canvas.getContext) {
    var ctx = canvas.getContext('2d');

    ctx.beginPath();
    ctx.moveTo(75, 50);
    ctx.lineTo(100, 75);
    ctx.lineTo(100, 25);
    ctx.fill();
  }
}
```

* 绘制直线
  * lineTo(x,y)：绘制一条从当前位置到指定x以及y位置的直线
* 圆弧
  * arc(x,y,radius,startAngle,endAngle,anticlockwise)：画一个以(x,y)为圆心，以radius为半径的圆弧，从startAngle开始到endAngle结束，按照anticlockwise给定的方向(默认顺时针)
  * arcTo(x1,y1,x2,y2,radius)：根据给定的控制点和半径画一段圆弧，再以直线连接两个控制点