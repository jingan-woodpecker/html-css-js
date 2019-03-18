```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
	   // window.onload = function() {}
	   // onload事件页面加载完触发该事件
	   onload = function() {
	   	   /*
          事件源.事件 = function() {
          // 事件处理函数
          }

	    */
	    // 找到事件源 ------- 根据id找元素
	    var oBtn = document.getElementById("btn");
        //alert(oBtn); 
        // onclick 单击
        oBtn.onclick = function() {
        	// 事件发生后会执行的操作
        	alert("你好啊");
        }
	   }
	    
	</script>
	<button id="btn">点我一下试试</button>
</body>
</html>
```