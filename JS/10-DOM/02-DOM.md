1、onchange时间：下拉框

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
    <select name="" id="sel">
        <option value="">请选择你需要的颜色</option>
        <option value="red">红色</option>
        <option value="green">绿色</option>
        <option value="blue">蓝色</option>
    </select>
    <p>字体颜色变化</p>
    <script>
        var oSel = document.getElementById("sel");
        var oP = document.getElementsByTagName("p")[0];

        oSel.onchange = function() {
            oP.style.color = this.value;
        }
    </script>
</body>
</html>
```

2、焦点事件(onfocus、onblur)

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<input type="text" id="txt"/>
	<span id="info"></span>
	<script type="text/javascript">
	     /*
             失去焦点时候 假如为空 提示 不能为空
                          假如非数字 提示 不合法
                          假如数字长度小于6 提示 "长度不够"
                          假如为数字  提示正确 

	     */
	     // var str = "   hello   ";
	     // console.log(str.trim().length);
	     var txt = document.getElementById("txt");
	     var info = document.getElementById("info");
	     // 获取焦点事件
	     txt.onfocus = function() {
	     	//alert("我获得了焦点");
	     	//console.log("我获得了焦点");
	     	this.value = "";
	     }
         // 失去焦点事件
	     txt.onblur = function() {
	     	// 进行数据校验
	     	// 拿到数据
	     	//alert(this.value); trim()去掉头尾空格
	     	var val = this.value.trim();
	     	if (val === "") {	
                info.innerHTML = "不能为空";
                info.style.color = "red";
                return;
	     	} 
	     	if (isNaN(val)) {
                info.innerHTML = "必须是纯数字";
                info.style.color = "red";
                return;
	     	}
	     	if (val.length < 6) {
                info.innerHTML = "长度不能小于6";
                info.style.color = "red";
                return;
	     	}
	     	// 上面都不满足 说明合法
	     	info.innerHTML = "正确";
	     	info.style.color = "green";
	     }
	</script>
</body>
</html>
```

3、h5中dom元素的查找方式(querySelector、querySelectorAll)

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<div>我是div1</div>
	<div id="box2" class="box2">我是div2</div>
	<script type="text/javascript">
	    // querySelector() 只返回满足条件的第一个元素 
	    // 兼容 ie8+
		// 1、querySelector只返回匹配的第一个元素，如果没有匹配项，返回null。 
		// 2、querySelectorAll返回匹配的元素集合，如果没有匹配项，返回空的nodelist(节点数组)。 
		// 3、返回的结果是静态的，之后对document结构的改变不会影响到之前取到的结果。 
 
	    var oDiv = document.querySelector("div");
	    var oDivs = document.querySelectorAll("div");
	    var box2 = document.querySelector("#box2");
	    //alert(oDiv.innerHTML);
	    //alert(oDivs.length);
	    alert(box2.innerHTML);
	</script>
</body>
</html>
```

4、全选与反选框操作
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
    <input type="checkbox" name="checkAll">全选<br>
    <input type="checkbox" name="fx">反选<br>
    <input type="checkbox" name="cl">python
    <input type="checkbox" name="cl">java
    <input type="checkbox" name="cl">php
    <input type="checkbox" name="cl">c++

    <script>
        var checkAll = document.getElementsByName("checkAll")[0];
        var fx = document.getElementsByName("fx")[0];
        var cls = document.getElementsByName("cl");

        checkAll.onclick = function() {
            for(var i=0; i<cls.length; i++) {
                cls[i].checked = this.checked;
            }
        }

        fx.onclick = function() {
            for(var i=0; i<cls.length; i++) {
                cls[i].checked = !cls[i].checked;
                checkAll.checked = false;
            }
        }

        for(var i=0; i<cls.length; i++) {
            cls[i].onclick = function() {
                var countChecked = 0;
                for(var j=0; j<cls.length; j++) {
                    if(cls[j].checked) {
                        countChecked++;
                    }
                }
                if(countChecked == cls.length) {
                    checkAll.checked = true;
                } else {
                    checkAll.checked = false;
                }
            }
        }
    </script>
</body>
</html>
```