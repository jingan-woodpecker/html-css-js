一、DOM节点删除

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<ul>
		
	</ul>
	<button>点我删ul</button>
	<script type="text/javascript">
	    var ul = document.querySelector("ul");
	    var li = document.createElement("li");
	    li.innerHTML = "我是li";
        ul.appendChild(li);
        // 绑定事件
        var btn = document.querySelector("button");
        btn.onclick = function() {
        	// 删除ul
        	ul.remove();
        }
	</script>
</body>
</html>
```

二、动态创建表格

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    行：<input type="text" id="row">
    列：<input type="text" id="col">
    <button id="btn">创建</button>

    <div id="wrap">

    </div>
    <script>
        function $(id){
            return document.getElementById(id);
        }

        $("btn").onclick = function() {
            $("wrap").innerHTML = "";
            var row = $("row").value;
            var col = $("col").value;
            var oTable = document.createElement("table");
            oTable.border = "1";
            oTable.style.width = "300px";
            oTable.style.height = "300px";

            for(var i=0; i<row; i++) {
                var oTr = document.createElement("tr");

                for(var j=0; j<col; j++) {
                    var oTd = document.createElement("td");
                    oTr.appendChild(oTd);
                }
                var endTd = document.createElement("td");
                endTd.innerHTML = "<a href='javascript:;'>删除</a>";
                oTr.appendChild(endTd);
                oTable.appendChild(oTr);
            }
            $("wrap").appendChild(oTable);
            var as = oTable.querySelectorAll("a");
            for(var i=0; i<as.length; i++) {
                as[i].onclick = function() {
                    if(confirm("你确定删除？")) {
                        this.parentNode.parentNode.remove();
                        if(oTable.children.length === 0) {
                            oTable.remove();
                        }
                    }
                }
            }
        }

    </script>
</body>
</html>
```

三、创建文本节点
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<div></div>
	<script type="text/javascript">
	     var oTxt = document.createTextNode("<h1>我是文本</h1>");
	     var oDiv = document.querySelector("div");
	     // 给div元素添加文本节点
	     oDiv.appendChild(oTxt);
	     //oDiv.innerText = "<p>1234</p>"; // 把标签当文本对待
	</script>
</body>
</html>
```

四、任意位置插入节点

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<ul>
		
	</ul>
	<button>添加一项</button>
	<script type="text/javascript">
	    var ul = document.querySelector("ul");
	    var btn = document.querySelector("button");
	    var i = 0;
	    btn.onclick = function() {
	    	var li = document.createElement("li");
	    	li.innerHTML = "我是li"+(++i);
        	//ul.appendChild(li);
			// insertBefore() 方法在您指定的已有子节点之前插入新的子节点
			// document.getElementById("myList").insertBefore(newItem,existingItem);
        	ul.insertBefore(li,ul.children[0]);
	    }
	    
	</script>
</body>
</html>
```

五、节点的复制

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<div>
		<p>我是一段落</p>
	</div>
</body>
</html>
<script type="text/javascript">
	    var oDiv = document.querySelector("div");
	    //var divClone = oDiv.cloneNode();// 浅复制  只复制父亲 子元素不复制
	    var divClone = oDiv.cloneNode(true);
	    document.body.appendChild(divClone);// 
</script>
```

六、节点的克隆应用

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<table border="1" id="tb">
		<!-- 有个隐藏的tbody标签 -->
		<tr>
			<td><input type="checkbox"></td>
			<td>姓名</td>
			<td>性别</td>
			<td>年龄</td>
		</tr>
	</table>
    姓名:<input type="text" id="userName" />
    性别: <input type="radio" name="sex" id="d" />男
    <input type="radio" name="sex" />女
    年龄: <input type="text" name="" id="age" />
    <input type="button" id="saveBtn" value="保存" />
    <script type="text/javascript" src="./public.js"></script>
    <script type="text/javascript">
         $("saveBtn").onclick = function() {
         	 // 复制第一行
         	var tr = $("tb").children[0].children[0].cloneNode(true);
         	// 添加到表格
         	$("tb").appendChild(tr);
         	// 修改当前复制行的内容
         	tr.children[1].innerHTML = $("userName").value;
         	var sex = $("d").checked?"男":"女";
         	tr.children[2].innerHTML = sex;
         	tr.children[3].innerHTML = $("age").value;
         }
    </script>
</body>
</html> 
```

七、节点的文档碎片

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	
	<script type="text/javascript">
	    // 页面放置500个p元素  '我爱你'
	    // for(var i=0; i<1500; i++) {
	    // 	 var oP = document.createElement("button");
     //         oP.innerHTML = "我爱你";
     //         document.body.appendChild(oP);
	    // }

	    // var str = "";
	    // for(var i=0; i<1500; i++) {
	    // 	str += "<button>我爱你</button>";
	    // }
	    // // 一次添加到body
	    // document.body.innerHTML = str;
         
         // 创建缓存
         var cache = document.createDocumentFragment();
         for(var i=0; i<1500; i++) {
         	var btn = document.createElement("button");
         	btn.innerHTML = "我爱你";
         	cache.appendChild(btn);
         }
         document.body.appendChild(cache);
         
	</script>
</body>
</html>
```