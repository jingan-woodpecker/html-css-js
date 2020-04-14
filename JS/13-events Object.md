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
    pageX   pageY   以文档页面为准（加上滚动条不可见区域）

