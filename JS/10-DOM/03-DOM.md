一、图片切换

```html

<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>图片轮播的两种方式</title>
	<style>
		#controls {
			width:400px;
			margin: auto;
			text-align: center;
		}
		#container {
			width: 400px;
			height:400px;
			border: 10px solid #eee;
			position: relative;
			background: gray;
			margin: 10px auto 0;
		}
		#prev, #next {
			position: absolute;
			background: black;
			/* 使用透明度标签会出现下划波浪线报错 */
			/* filter:alpha(opacity:40); */
			opacity: 0.4;
			font-size: 20px;
			color: white;
			width: 40px;	
			height: 40px;
			border: 2px solid white;
			line-height: 40px;
			text-align: center;
			top: 180px;
			pointer: cursor;
			text-decoration: none;
		}
		#prev:hover, #next:hover {
			/* filter:alpha(opacity:80); */
			opacity: 0.8;
		}
		#order, #info {
			position: absolute;
			width:100%;
			height: 30px;
			line-height: 30px;
			text-align: center;
			background: black;
			/* filter:alpha(opacity:60); */
			opacity: 0.6;
			font-size: 20px;
			color: white;
		}
		#prev {
			left: 0;
		}
		#next {
			right: 0;
		}
		#picture {
			height: 400px;
			width: 400px;
		}
		#order {
			top: 0;
		}
		#info {
			bottom: 0;
		}
	</style>
	
		
</head>
<body>
	<div id="controls">
		<input id="round" type="button" value = "循环播放">
		<input id="single" type="button" value = "顺序播放">
	</div>
	<div id="container">
        <a href='javascript:' id="prev">&lt;</a>
        <a href='javascript:' id="next">&gt;</a>
        <div id="order">图片加载中……</div>
        <div id="info">图片加载中……</div>	
        <img id="picture">
	</div>
	<script type="text/javascript">
	    // 封装一个函数  根据id找元素
	    function $(id) {
	    	return document.getElementById(id);
	    }
	    // 定义一个数组 存放图片路径
	    var imgsArr = ["6.jpg","7.jpg","8.jpg","9.jpg"];
	    var imgsText = ["图片一","图片二","图片三","图片四"];
	    var index = 0;
        var flag = true;// 值为true 默认为顺序播放 
        // 定义显示信息
        function showInfo() {
        	$("picture").src = imgsArr[index];
        	$("order").innerHTML = (index+1)+"/4";
        	$("info").innerHTML = imgsText[index];
        }
        showInfo();

	    // 给左箭头绑定事件
        $("prev").onclick = function() {
              index--;
              // 是顺序播放 并且index为-1
              if (flag && index === -1) {
              	   alert("已经是第一张了");
              	   index = 0;
              } else if( !flag && index === -1) {
                   index = imgsArr.length - 1;
              }
              showInfo();
        } 

        // 给右箭头绑定事件
        $("next").onclick = function() {
        	index++;
        	// 顺序播放
        	if (flag && index === imgsArr.length) {
        		alert("已经是最后一张了");
        		index = imgsArr.length - 1;
        	} else if (!flag && index === imgsArr.length) {// 循环播放
                index = 0;
        	}
        	showInfo();
        }

        $("round").onclick = function() {
        	alert("开始循环播放了");
        	flag = false;
        }

        $("single").onclick = function() {
        	alert("开始顺序播放了");
        	flag = true;
        }
	</script>
</body>
</html>
```

二、获取父节点元素名称

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<table border="1" id="tb">	
		<tr id="tr1">
			<td>111</td>
			<td>1111</td>
			<td>
				<input type="button" value="删除" />
			</td>
		</tr>
		<tr id="tr2">
			<td>222</td>
			<td>2222</td>
			<td>
				<input type="button" value="删除" />
			</td>
		</tr>
	</table>
	<script type="text/javascript">
	   var btns = document.getElementsByTagName("input");
	   /* obj.parentNode 父节点*/
	   for(var i=0; i<btns.length; i++) {
	   	     btns[i].onclick = function() {
                 alert(this.parentNode.parentNode.nodeName);
	   	     }
	   }

	   var tb = document.getElementById("tb");
	   //alert(tb);
	   alert(tb.firstChild);// [object Text] 文本对象 会把文本也看成自己的儿子
	   alert(tb.firstElementChild.tagName); // TBODY
	   
	</script>
</body>
</html>
```

三、元素节点儿子包括文本和标签（childNodes）、只包含元素节点儿子（children）

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<ul>
		<li>aaaa</li>
		<li>bbbbbb</li>
		<li>cccc</li>
		<li>ddddd</li>
		<li>eeeee</li>
	</ul>
	<script type="text/javascript">
	    // 
	    var oUl = document.querySelector("ul");
	    //var lis = oUl.childNodes; // 所有的儿子 包括文本和标签
	    //alert(lis.length); // 11
	    /* 对所有的li增加字体颜色样式 red
	    for(var i=0; i<lis.length; i++) {
	    	// 元素的nodeType值为1 表示元素节点
	    	if (lis[i].nodeType === 1) {
                lis[i].style.color = "red";
	    	}
	    }
	    */

	    var lis = oUl.children; // 只包含元素节点儿子
	    alert(lis.length);
	</script>
</body>
</html>
```

四、DOM节点创建(createElement、appendChild)

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style type="text/css">
	   .box {
	   	  width: 200px;
	   	  height: 200px;
	   	  border: 1px solid #ccc;
	   }
	</style>
</head>
<body>
	
	<script type="text/javascript">
	    // 创建div元素
	    var oDiv = document.createElement("div");
	    // 将创建好的元素添加到body中
	    document.body.appendChild(oDiv);
	    // 设置样式和文本
	    oDiv.innerHTML = "我是动态创建的div";
	    oDiv.className = "box";
	</script>
</body>
</html>
```

动态创建星星

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style type="text/css">
	    * {
	    	padding: 0;
	    	margin: 0;
	    }
	    body {
	    	background: #000;
	    }
	    /*img {
	    	width: 20px;
	    	height: 20px;
	    }*/
	</style>
</head>
<body>
	<script type="text/javascript">
	    //  js在文档中创建图片
	    var oImg = document.createElement("img");
	    oImg.src = "star.jpg";
	    document.body.appendChild(oImg);
	    // 设置图片宽度为随机的 20~30
	    var w = parseInt(Math.random()*11+20);
	    //console.log(w);
	    //oImg.style.width = oImg.style.height = w + "px";
	    oImg.width = oImg.height = w;
	</script>
</body>
</html>
```