# （一）canvas 

## 1、canvas 简介

1、`<canvas>` 标签是 `HTML5` 新增的，一个可以使用脚本(通常为 `JavaScript`) 在其中绘制图像的 `HTML` 元素。它可以用来制作照片集或者制作简单(也不是那么简单)的动画，甚至可以进行实时视频处理和渲染。

2、基本使用

```html
<canvas id="tutorial" width="300" height="300"></canvas>
```

3、[官网]([学习 HTML5 Canvas 这一篇文章就够了 | 菜鸟教程 (runoob.com)](https://www.runoob.com/w3cnote/html5-canvas-intro.html))

## 2、常用属性

|   关键词    |         用法          |
| :---------: | :-------------------: |
|  beginPath  |     闭合图形开始      |
|   moveTo    |    定义图形初始值     |
|   lineTo    | 定义图形第N个点的位置 |
| strokeStyle |   定义图形边框颜色    |
|  lineWidth  |   定义图形边框宽度    |
|  fillStyle  |     定义填充颜色      |
|    fill     |       进行填充        |
|             |                       |
|   stroke    |       进行绘制        |
|  closePath  |     闭合图形结束      |



|  关键词   |                   属性内的值                    |       用法       |
| :-------: | :---------------------------------------------: | :--------------: |
| clearRect |    （ 起始点X轴 ， 起始点Y轴 ， 宽 ， 高 ）     | 所选区域进行清除 |
| fillRect  |    （ 起始点X轴 ， 起始点Y轴 ， 宽 ， 高 ）     |     填充矩形     |
|   rect    |    （ 起始点X轴 ， 起始点Y轴 ， 宽 ， 高 ）     |     矩形边框     |
|    arc    | (起始点的X轴,起始点的Y轴,半径,起始点,终点,方向) |     填充圆弧     |
|           |                                                 |                  |
|           |                                                 |                  |
|           |                                                 |                  |



## 1、创建一个画板

```HTML
<style>
        *{
            margin:0px;
            padding: 0px;
        }
</style>
<body>
    <canvas id="container" width="500" height="300" style="border: 1px solid red;"></canvas>
</body>
<script>
//思路：线段的初始值与鼠标按键按下的位置绑定，页面中的笔画与鼠标移动的轨迹绑定
    //获取节点
    var divs = document.getElementById("container");
    //设定一条线段
    var context = divs.getContext("2d");
    //创建鼠标按键按下事件
    divs.onmousedown = function (e) {
    // console.log(e);
    //设置画笔颜色
    context.strokeStyle='blue';
    //设置画笔宽度
    context.lineWidth='1';
    context.moveTo(e.clientX, e.clientY);
    //创建鼠标按键移动事件
    divs.onmousemove = function (f) {
        // console.log(f);
        //页面中的笔画绑定为鼠标移动的轨迹
    context.lineTo(f.clientX,f.clientY)
    context.stroke();
  };
        //创建鼠标按键松开事件
        divs.onmouseup = function(){
            divs.onmousemove=null
	  }
    };
</script>
```



## 2、创建一个三角形

```html
<style>
		*{
			margin:0px;
			padding: 0px;
		}
</style>
<body>
	<canvas id="container" width="500" height="300" style="border: 1px solid red;"></canvas>
</body>
<script type="text/javascript">
//思路：创建三条线段组成一个三角形
		//获取节点
		var divs = document.getElementById("container");
		//设定一条线段
		var context = divs.getContext("2d");
		//闭合图形开始
		context.beginPath();
		//定义图形初始值
		context.moveTo(50, 10);
		//定义图形第二个点的位置
		context.lineTo(10, 50);
		//定义图形第三个点的位置
		context.lineTo(90,50);
		//定义图形结尾的位置
		context.lineTo(50, 10);
		//定义图形边框颜色
		context.strokeStyle='red';
		//定义填充颜色
		context.fillStyle = 'blue' 
		//开始填充
		context.fill()
		//进行绘制
		context.stroke();
		//闭合图形结束
		context.closePath();
</script>
```



## 3、创建一个四边形

### 方法1：创建一个矩形，再进行填充

```html
<style>
    *{
        margin:0px;
        padding: 0px;
    }
</style>
<body>
	<canvas id="container" width="500" height="300" style="border: 1px solid red;"></canvas>
</body>
<script type="text/javascript">
		//获取节点
		var divs = document.getElementById("container");
		//设定一条线段
		var context = divs.getContext("2d");
    	//闭合图形开始
		context.beginPath();
		//初始X轴位置,初始Y轴位置,图形宽度,图形高度
		context.rect(50,50,100,50)
		//定义边框颜色
		context.strokeStyle='#000';
		//定义填充颜色
		context.fillStyle='pink';
		//进行填充
		context.fill()
		//进行绘制
		context.stroke()
		//闭合图形结束
		context.closePath()
</script>
```

### 方法2：创建填充的区域，区域设置为矩形

```html
<style>
    *{
        margin:0px;
        padding: 0px;
    }
</style>
<body>
	<canvas id="container" width="500" height="300" style="border: 1px solid red;"></canvas>
</body>
<script type="text/javascript">
		//获取节点
		var divs = document.getElementById("container");
		//设定一条线段
		var context = divs.getContext("2d");
    	//闭合图形开始
		context.beginPath();
		//定义填充颜色
		context.fillStyle='green';
		//初始X轴位置,初始Y轴位置,图形宽度,图形高度
		context.fillRect(100,100,150,60);
		//所选区域进行清除
		context.clearRect(120,120,75,30)
		//闭合图形结束
		context.closePath();
</script>
```



## 4、创建一个圆形

```html
<style>
		*{
			margin:0px;
			padding: 0px;
		}
</style>
<body>
	<canvas id="container" width="500" height="300" style="border: 1px solid red;"></canvas>
</body>
<script>
	   //获取节点
		var divs = document.getElementById("container");
		//设定一条线段
		var context = divs.getContext("2d");
		//闭合图形开始
		context.beginPath();
		//起始点的X轴,起始点的Y轴,半径,起始点,终点,方向
	    context.arc(100,100,50,0,Math.PI/180*360,false);
	    context.fill();
	    //闭合图形结束
	    context.closePath();
</script>
```



## 5、创建渐变色图形

```html
<style>
		*{
			margin: 0px;
			padding: 0px;
		}
	</style>
	<body>
	<canvas id="container" width="500" height="300" style="border: 1px solid red;"></canvas>
</body>
<script>
		//获取节点
		var divs = document.getElementById("container");
		//设定一条线段
		var context = divs.getContext("2d");
		//先创建渐变色
		var gb = context.createLinearGradient(100, 150, 100, 50);
		gb.addColorStop(0, 'blue');
		gb.addColorStop(0.5, 'green');
		gb.addColorStop(1, 'yellow');
		//再创建图形
		context.beginPath();
		context.arc(100,100,80,0,360*Math.PI/180,true);
		//填充方式引用创建的渐变色
		context.fillStyle=gb;
		context.fill();
		context.closePath();
</script>
```



