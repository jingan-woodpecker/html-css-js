一、window对象setInterval异步定时器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        // 每隔一段时间就执行一段代码一次 全称window.setInterval
        // 语法与setTimeout类似，经过几秒就执行一段代码，但这个对象重复执行
        // 函数作为参数传给另一个函数叫高阶函数

        setInterval(function() {
            alert("每隔两秒就弹窗一次");
        }, 2000);

        // 其它方式使用，逻辑较复杂使用下面的方面
        // 先将要执行操作的函数放到外面
        function fn() {
            alert("每隔两秒就弹窗一次");
        }
        // 再将上面定义好的函数名传入定时器函数
        // 注意传入下面定时器的是函数fn，而不是fn()
        // fn()这种叫做函数的调用，最后会得到一个返回值传到定时器
        // 上面函数没有返回值，就会返回undefinde

        setInterval(fn(),2000);  // 错误的写法
        setInterval(fn, 2000);   // 正确的写法
        setInterval("fn()",2000);// 正确的写法 了解

    </script>
</body>
</html>
```

二、应用

    常用：轮播图、倒计时
    使用定时器前先学习日期对象

    日期对象

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        var now = new Date(); // new新创建当前日期对象
        //console.log(now); // 包含日期、时间、时区等信息

        // 获取年月日
        var year = now.getFullYear();
        var month = now.getMonth();
        // alert(month); 
        // 注意：因为西方国家定义0-11为12个月份，0表示一月，要想符合中文习惯就加1
        var day = now.getDate();

        //获取时分秒
        var hour = now.getHours();
        var minutes = now.getMinutes();
        var second = now.getSeconds();
        alert(hour+":"+minutes+":"+second);
    </script>
</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        var now = new Date(); // new新创建当前日期对象
        //console.log(now); // 包含日期、时间、时区等信息

        // 获取星期几
        // alert(now.getDay);  0-6 0代表周日 通过定义数组weekArr转换成符合中文习惯的星期几

        // 将now放进去，后面d就是now
        var text = dateToString(now);
        alert(test);
        // 定义一个函数将日期格式转换成字符串
        // 先传入一个日期对象d
        function dateToString(d) {
            // 定义个数组，获取星期几，第一个下标0写星期日，跟上面0-6，0代表星期日对应
            var weekArr = ["星期日","星期一","星期二","星期三","星期四","星期五","星期六"];
            // 获取年月日
            var year = d.getFullYear();
            var month = d.getMonth()+1;
            // alert(month); 
            // 注意：因为西方国家定义0-11为12个月份，0表示一月，要想符合中文习惯就加1
            var day = d.getDate();

            //获取时分秒
            var hour = d.getHours();
            var minutes = d.getMinutes();
            var second = d.getSeconds();

            // 注意回车换行拼接字符串需要加个空字符串
            var str = year + "年" + month + "月" + day + "日" + " ";
            str += h + ":" + m + ":" + s;
            str += " " + weekArr[d.getDay()];
            return str;     
        }
    </script>
</body>
</html>
```

    