一、window对象

    （1）可在控制台输入：window 就会显示大部分对象
    例如：window.alert("ok"),其中window可以省略

![window](../picture/window1.png)

    （2）定义的全局变量会挂载到window的对象下
    （3）定义的全局函数同样也会

```html
<script>
    var d = 100;
    alert(d);
    // alert(window.d) 跟上面的效果一致

    function fn() {
        alert(3);
    }
    fn()
    // window.fn() 跟上面效果一致
</script>
```
![windows2](../picture/window2.png)

二、常用window对象

    弹窗：confirm() prompt() alert()
    定时器:setTimeout 每隔一段时间，执行某个函数的操作（不会重复执行，只执行一次操作）

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
    <script>
        // 隔一秒钟显示i的值，时间的单位是毫秒，此例子为匿名函数也是函数
        var i = 0;
        window.setTimeout(function(){
            document.write(i);
        },1000)
    </script>
</body>
</html>
```

    清除和取消定时广告实例

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
    <button id="btn">清除广告</button>
    <button id="btnStop">取消</button>
    <img id="pic" src="picture/hua1.jpg" alt="花盆">

    <script>
        var btn = document.getElementById("btn");
        var get_img = document.getElementById("pic");
        // querySelector里面写的是css属性值
        var btnStop = document.querySelector("#btnStop")
        // 设置一个全局的变量timer，单击清除广告按钮时记住当前状态，单击取消就清除这个状态；
        // 不可设置为局部变量，因为不止绑定清除广告事件需要调用，取消绑定事件也需要使用
        var timer = null;
        btn.onclick = function() {
            // 记住这个状态
            timer = setTimeout(function() {
                get_img.style.display = "none";
            },3000);
        }

        // 取消绑定事件
        btnStop.onclick = function() {
            // 清除上面保存的状态
            clearTimeout(timer)
        }
        
    </script>
</body>
</html>
```

三、定时器异步问题

    异步：事件回调、定时器、ajax、node（绝大部分是异步的）
    同步：只能前面一件事执行完，再执行下一件事情   