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