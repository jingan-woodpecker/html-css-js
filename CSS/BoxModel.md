>盒模型

    比如一个相框 400*400的相框以及300*300的相片
    width----------------内容的宽度，不是盒子的总宽度
    height---------------内容的高度，不是盒子的总高度
    border---------------边框
    padding--------------内边距
    margin---------------外边距
    
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
<head>
	<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
	<title>Document</title>
	<style type="text/css">
		div {
			width: 200px;
			height: 200px;
			padding: 100px;
			border: 10px solid blue;
			margin-top: 200px;
			background-color: red; 
		}
	</style>
</head>
<body>
	<div>
		江南的风轻轻的吹，那样柔软，那样舒适，吹过青青芳草地，吹过盈盈碧水岸，吹过烟雨蒙蒙的江南杨柳舍。江南的风如此温柔，轻轻吹过我柔柔的发间，轻轻吹过我湿润的双眸；江南的风如此温暖，我灵敏的鼻息仿佛嗅到你谈吐间暖暖的气息
	</div>
</body>
</html>
```
![盒模型](../picture/box01.png)

    上面的盒子真实宽度是多少？   200+100+100+10+10=420px
>1、padding属性

    内容和边框之间的距离：
        padding: 10px;
        相当于padding-top: 10px;
             padding-right: 10px;
             padding-buttom: 10px;
             padding-left: 10px;
        
        padding: 10px 20px; 上（下）10px， 右（左）20px；
        padding: 10px 20px 30px; 上10px， 右(左)20px， 下30px;
        padding: 10px 20px 30px 40px 上10px, 右20px, 下30px, 左40px;
        
        记忆规律：四个值的时候就顺时针书写；
                不满四个值时，先按顺序写完，缺少的找对立面即可；
                比如：padding: 10px 20px; 先按顺序写上10px,右20px,缺少的找对立面，上对应下也10px,右对应左也20px

**注意自带padding和margin对网页的制作影响**                
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
<head>
	<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
	<title>Document</title>
	<style type="text/css">
	/*由于ul自带padding和margin对我们页面制作有影响
	所以我们需要重置清零*/
	* {
		padding: 0;
		margin: 0;
	}
	</style>
</head>
<body>
	<ul>
		<li>自动化测试</li>
		<li>性能测试</li>
		<li>功能测试</li>
		<li>稳定性测试</li>
	</ul>
</body>
</html>
``` 
![padding](../picture/padding.png)
![padding](../picture/padding01.png)   

>2、border属性

    边框三要素： 粗细、线型、颜色
    border: 10px solid blue;
    对应于：
        border-width: 10px;
            分解： border-top-width: 10px;
                  border-right-width: 10px;
                  border-buttom-width: 10px;
                  border-left-width: 10px;
                  
        border-style: solid;
            分解：......
        border-color: blue;
            分解：......
    
    常用线型：solid------实线
            dashed-----虚线
            其余线型容易出现兼容性问题       