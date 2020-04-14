一、事件对象概念

    与事件相关的对象，事件（比如：鼠标单击、双击等）发生后，浏览器会传一个
    对象给事件处理函数，该对象封装了与该事件相关的信息（比如：clientX/clientY等可以在控制台查看）

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
        document.onclick = function(e) {
            // 参数e与当前事件onclick鼠标事件有关
            alert(e);
        }
    </script>
</body>
</html>
```

二、兼容处理事件对象

    原则：先处理高级浏览器，后低级浏览器
    比如下面的e事件对象写在前面，先处理的高级浏览器，再加上event事件对象处理低级浏览器

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
        document.onclick = function(e) {
            // 参数e与当前事件onclick鼠标事件有关
            var event_compatibility = e || event;
            console.log(event_compatibility);
        }
    </script>
</body>
</html>
```

三、事件对象常用的坐标属性

    screenX screenY 离电脑屏幕的距离
    clientX clientY 可视区域（就是文档页面可以看见的区域）
    pageX   pageY   以文档页面为准（加上滚动条不可见区域）——常用
    offsetX offsetY 相对于盒子的距离

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        /* 设置滚动条 */
        body {
            height: 2000px;
        }

        div {
            width: 200px;
            height: 200px;
            background-color: pink;
        }        
    </style>
</head>
<body>
    <div></div>
    <script>
        document.onclick = function(e) {
            // 先兼容处理
            var events = e || event;
            console.log(events.clientX + ":" + events.clientY);
            console.log(events.pageX + ":" + events.pageY);
            // console.log(events.screenX + ":" + events.screenY);
        }

        var oDiv = document.querySelector("div");
        oDiv.onmouseover = function(e) {
            var e = e || event;
            // 相对于盒子的距离
            console.log(e.offsetX + ":" + e.offsetY);
        }
    </script>
</body>
</html>
```

四、应用：图片跟随效果

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
            img {
                position: absolute;
            }
    </style>
</head>
<body>
    <img src="images/love.jpg" width="50" alt="">
    <script type="text/javascript">
        var oImg = document.querySelector("img");
        // 函数传入一个参数e，要用到坐标信息，因为信息是封装在这个事件对象里面
        // 注意是文档document绑定，不是图片img
        document.onmousemove  = function(e) {
            // 鼠标移动获取到位置进行移动，绑定鼠标移动事件
            // 先兼容
            var events = e || window.event;
            // 获取鼠标坐标
            var x = events.pageX;
            var y = events.pageY;
            // 鼠标坐标值减去对应的盒子的一半宽高
            // 宽度高度是元素固有的属性，所以可以直接(元素.属性)的方式调用，例如oImg.width
            oImg.style.left = x - oImg.width/2 + "px";
            oImg.style.top = y - oImg.height/2 + "px";
        }
    </script>
</body>
</html>
```

五、button属性（注意是属性不是元素）

    onmousedown 鼠标按下事件（左键、滚轮、右键）
    高版本谷歌、火狐、ie浏览器按下左键显示0，滚轮显示1，右键显示2
    对于ie8及以下浏览器 1 左键、4滚轮、2右键

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
        document.onmousedown = function(e) {
            // 事件对象兼容，低版本只识别event
            // var e = e || event
            // 可以根据获取的数值来确定用户的行为是左击还是右击等
            // 获取到用户行为后，比如左击之后就做其它行为
            // alert(e.button);

            alert(getButton(e))
        }

        // 封装一个函数识别浏览器，e形参代表事件处理函数的形参
        function getButton(e) {
            // 能力检测
            if (e) {
                // 可以识别高版本浏览器，依然返回e.button
                return e.button;
                //如果识别到低版本，需要跟高版本统一
            } else if (window.event) {
                switch(event.button) {
                    case 1: return 0;
                    case 4: return 1;
                    case 2: return 2;
                }
            }
        }
    </script>
</body>
</html>
```

    字体图标网址：https://fontawesome.dashgame.com/  下载 解压
    查看网站如何使用字体图标




