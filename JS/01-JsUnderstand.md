1、JS概述

    *负责页面的交互和行为
    
    *作用
        (1)数据验证
        (2)操作html元素
        (3)制作网页特效(轮播、其它效果)
        (4)WEB游戏
        (5)Nodejs进行服务端编程
        
    *组成部分
        a 语言核心 ECMAscript 如变量 数组 函数 对象...
        b DOM 文档模型对象
        c BOM 浏览器模型对象
        
二、js书写位置

        一、内嵌式
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
		alert("javascript");
	</script>
</body>
</html>
```
       二、行内式
       三、外链式
       
三、常用语句

        alert("....");  弹窗语句，双引号里面的内容会出现在弹出的窗口中
        ;是js语句结束的标志(不加分号，上线压缩文件后，就无法识别哪里表示结束语句)

        prompt对话框
        弹出一个对话框，允许用户输入内容 
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
		// 其中"18839450404"为默认值
		var v1=prompt("请输入你的电话号码","18839450404")
		alert(v1);
	</script>
</body>
</html>
```
        
        console控制台
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
		console.log(123);
		console.log("abc")
		console.error("错误信息")
		console.warn("警告信息")
	</script>
</body>
</html>
```

四、注释

    单行注释符号： "//"
    多行注释符号： "/*  */
    不允许多行套多行注释



    

        