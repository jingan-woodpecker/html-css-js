一、操作节点属性

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<div id="box" msg="hello" class="box">我是div</div>
	<script type="text/javascript">
	    // 获取div元素的id属性值
	    var oDiv = document.querySelector("div");
	    //alert(oDiv.id); // 元素.属性 获取的是固有属性 不能获取自定义属性
	    alert(oDiv.className); // 注意 获取class属性 js应该为className
	    //alert(oDiv.msg);
	    //var id = oDiv.getAttribute("id");
	    // getAttribute("msg") 可以获取固有属性也可以获取自定义属性
	    //var msg = oDiv.getAttribute("msg");
	    //alert(msg);
	    // 设置属性
	    oDiv.setAttribute("id","wrap");
	    oDiv.setAttribute("abc","123");

	    //  删除属性
	    oDiv.removeAttribute("class");
	</script>
</body>
</html>
```

二、选项卡效果

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>选项卡</title>
		<style type="text/css">
			*{margin: 0; padding: 0; font-family: "微软雅黑";font-size: 14px;}
			#container{
				width: 398px; 
				margin: 100px auto;}
			#container a{
				display:block ;
				width: 98px; 
				height: 42px; 
				line-height: 42px; 
				text-align: center; 
				float: left;
				border-top: solid 1px #FF4400;
				border-bottom: solid 1px #FF4400;
				border-left: solid 1px #FF4400;
				color: #333333;
				text-decoration: none;
			}
			#container a:hover{
				color: #FF4400;
			}
			.content{
				width: 355px;
				height: 140px;
				text-align: center;
				border-right: solid 1px #FF4400;
				border-bottom: solid 1px #FF4400;
				border-left: solid 1px #FF4400;
				padding: 30px 0 0 40px;
				display: none;
			}
			.clear{clear: left;}
			#container a.on{ background: #FF4400; color: #fff;}
		</style>
	
	</head>
	<body>
		<div id="container">
			<a href="#"  class="on">充话费</a>
			<a href="#" >充流量</a>
			<a href="#" >充固话</a>
			<a href="#"  style="border-right: solid 1px #FF4400;">充宽带</a>

			<div class="clear"></div>
			
			<div class="content" style="display:block;">
				<img src="images/1.png" />
			</div>
			<div class="content">
				<img src="images/2.png" />
			</div>
			<div class="content">
				<img src="images/3.png" />
			</div>

			<div class="content">
				<img src="images/4.png" />
			</div>
		</div>
	</body>
</html>
<script type="text/javascript">
	 // 找到所有的导航
	 var container = document.getElementById("container");
	 var as = container.getElementsByTagName("a");
	 // 找到所有内容
	 var oDivs = document.getElementsByClassName("content");
	 // 给所有的a链接绑定事件
	 for(var i=0; i<as.length; i++) {
	 	as[i].setAttribute("index", i);
	 	//as[i].index = i; // 给对象动态增加一个属性
	 	as[i].onclick = function() {
	 		// 给当前的链接设置样式 其他的去除 ----排他思想
	 		// 先清除所有链接样式和让所有的内容div隐藏 
	 		for(var j=0; j<as.length; j++) {
	 			as[j].className = "";
                oDivs[j].style.display = "none";
	 		}
	 		// 对当前自己设置on样式
	 		this.className = "on";
	 		// 让对应的内容显示 0-0  1-1 2-2
	 		var index = this.getAttribute("index"); // 当前超链接的索引
	 		//var index = this.index;
	 		oDivs[index].style.display = "block";
	 	}
	 }
</script>
```

三、换肤效果

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
	<link rel="stylesheet" type="text/css" href="css/wolong.css" />
	<link rel="stylesheet" type="text/css" href="css/hs0.css" />
	<title></title>
</head>
	<script>
	    // 点击换肤 切换不同的图片 也就是引入不同的css
        window.onload = function() {
            var hf = document.getElementById("hf");
            var link = document.getElementsByTagName("link")[1];
            var index = 0;
            hf.onclick = function() {
                index++;
                if( index==5) {
                    index = 0;
                } 
                link.setAttribute("href", "css/hs"+index+".css");      
            }
        }
	</script>
<body>
<!--top-->
	<div class="top">     
            <input type="button" id="hf" value="换 肤"/>
            <input type="button" id="hy" value="还 原"/>
    	<div class="logo"><a href="#"><img src="images/wolong/logo1.jpg" /></a></div>
        <div class="search">
        	<div class=" searchcon">
            	<form method="post" action="">
                	<input class="txt" type="text" value="SEARCH……"/>
                    <input class="btn" type="submit" value=""/>
                </form>
            </div>
        </div>
    </div>
<!--nav-->
	<div class="nav">
    	<ul>
        	<li><a href="#">集团介绍</a></li>
            <li><a href="#">产品中心</a></li>
            <li><a href="#">卧龙市场</a></li>
            <li><a href="#">技术研发</a></li>
            <li><a href="#">国际合作</a></li>
            <li><a href="#">投资者关系</a></li>
            <li><a href="#">新闻资讯</a></li>
            <li><a class="lastb" href="#">人力资源</a></li>	
        </ul>
    </div>
    
<!--banner-->

	<div class="banner"><img src="images/wolong/banner.jpg" /></div>
<!--content-->
	<div class="content">
    	<div class="content1">
        	<div class="news">
            	<h3 class="bt">新闻资讯</h3>
                <ul class="newsul">
                	<li><a href="#">陈建成董事长出席ATB集团召开的年度销售大会</a><span>2013-07-10</span></li>
                    <li><a href="#">陈建成董事长出席ATB集团召开的年大会大会大会大会度销售大会</a><span>2013-07-10</span></li>
                    <li><a href="#">陈建成董事长出席ATB集团召开的年度销售大会</a><span>2013-07-10</span></li>
                    <li><a href="#">陈建成董事长出席ATB集团召开的年度销售大会</a><span>2013-07-10</span></li>
                    <li><a href="#">陈建成董事长出席ATB集团B集团B集团召开的年度销售大会</a><span>2013-07-10</span></li>
                    <li><a href="#">陈建成董事长出席ATBB集团召集团召开团召集团召开的年度销售大会</a><span>2013-07-10</span></li>
                </ul>
            </div>
            
            <div class="intro">
            	<h3 class="bt">卧龙介绍</h3>
                <p class="p1">公司成立于1984年,<br />经过近30年的发展</p>
                <p class="p2">已成为电器制造，房地产开发和金融<br />投资三业并举的综合性跨国……</p>
            </div>
            <div class="bringin">
            	<h3 class="bt">人才招聘</h3>
                <div class="txt">
                <p>培养一流的人才，铸造一流的工程</p>
                <p>实现员工与企业的共同发展</p>
                </div>
                <div class="more"><a href="#"><img src="images/wolong/more.jpg" /></a></div>
            </div>
        </div>
    <div class="content2">
    
    	<h3>卧龙市场<a href="#"><img src="images/wolong/jiankuohao1.jpg" /></a>&nbsp;<a href="#"><img src="images/wolong/jianjiao2.jpg" /></a></span></h3>
        
        <dl>
        	<dt><img src="images/wolong/jiaotong1.jpg" /></dt>
            <dd>
            	<p>交通轨道：由于主要采用电气牵引，而且轮轨摩擦阻力小，与公共交通……</p>
                
            </dd>
        </dl>
         <dl>
        	<dt><img src="images/wolong/jieneng1.jpg" /></dt>
            <dd>
            	<p>交通轨道：由于主要采用电气牵引，而且</p>
                <p>轮轨摩擦阻力小，与公共交通……</p>
            </dd>
        </dl>
         <dl>
        	<dt><img src="images/wolong/feiji1.jpg" /></dt>
            <dd>
            	<p>交通轨道：由于主要采用电气牵引，而且</p>
                <p>轮轨摩擦阻力小，与公共交通……</p>
            </dd>
        </dl>
         <dl>
        	<dt><img src="images/wolong/shiyou1.jpg" /></dt>
            <dd>
            	<p>交通轨道：由于主要采用电气牵引，而且</p>
                <p>轮轨摩擦阻力小，与公共交通……</p>
            </dd>
        </dl>
    </div>
    
    </div>
<!--links-->
<div class="links">
	
	<div class="product">
    	<h3 class="linksbt">产品中心</h3>
        <ul class="u1">
        	<li><a href="#">汽车电机</a></li>
            <li><a href="#">汽车电机</a></li>
            <li><a href="#">汽车电机</a></li>
            <li><a href="#">大功率电机</a></li>
            <li><a href="#">汽车电机</a></li>
        </ul>
        <ul class="u2">
        	<li><a href="#">工业驱动和自动化</a></li>
            <li><a href="#">高压变频和系统集成</a></li>
            <li><a href="#">混凝土搅拌机</a></li>
            <li><a href="#">电动车辆</a></li>
            
        </ul>
        <ul class="u3">
        	<li><a href="#">汽车电机</a></li>
            <li><a href="#">汽车电机</a></li>
            <li><a href="#">汽车电机</a></li>
            <li><a href="#">大功率电</a></li>
            
        </ul>
    </div>
    <div class="tec">
    	<h3 class="linksbt">技术研发</h3>
    	<ul class="u3">
        	<li><a href="#">汽车电机</a></li>
            <li><a href="#">汽车电机</a></li>
            <li><a href="#">汽车电机</a></li>
            <li><a href="#">大功率电</a></li>
            
        </ul>
    </div>
    <div class="net">
    	<h3 class="linksbt">营销网络</h3>
        
    </div>
</div>
<!--bottom-->
	<div class="bottom">
    	<div class="bnav">
        	<a href="#">网站地图</a>&nbsp;|
            <a href="#">联系我们</a>&nbsp;|
            <a href="#">关注卧龙</a>&nbsp;|
            <a href="#">系统采购入口</a>
        </div>
        <div class="btxt">
        	RIGHT&coopy;2013卧龙控股集团 版权所有 浙ICP备0658755677号 技术支持：博彩互动&nbsp;&nbsp;分享到：<a href="#"><img src="images/wolong/share01_03.jpg" /></a><a href="#"><img src="images/wolong/share01_05.jpg" /></a><a href="#"><img src="images/wolong/share01_07.jpg" /></a><a href="#"><img src="images/wolong/share01_09.jpg" /></a><a href="#"><img src="images/wolong/share_11.jpg" /></a>
        </div>
    </div>
</body>
</html>
```