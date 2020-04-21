面向对象  OOP Object Oriented Programming

    1 js对象
        狭义对象  就是用大括号{ }定义出来的就是狭义对象 
        可以添加属性 属性可以访问

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
        // 对象 一组无序的属性集合 狭义对象
        var xiaohong = {
            name: "小红",
            age: 18,
            hobby: ["coding", "eating"]
        };
        xiaohong.tel = "138888888";
        //alert(typeof xiaohong);
        //alert(xiaohong.age);
        alert(xiaohong.hobby[0]);
		
		// 对象的语义比数组更好，像下面的数值18从对象就可以看出是表示年龄，但是数组看不出
        var xiaohong = ["小红", 18, ["coding", "eating"]];
    </script>
</body>

</html>
```


    广义对象  window 、 Date 、Math
    本身是对象，可以直接通过打点添加属性，例如下面的正则
    本身是对象就可以直接添加属性、方法


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
    <div class="box"></div>
<body>
    <script>
        var box = document.querySelector("div");
        console.dir(box);  // DOM是对象
        box.name = "xiaoli";
        alert(typeof box);  // DOM添加其他属性后依然是对象object

        var reg = /\d/g;
        reg.name = "xiaohua";
        reg.age = 20;
        console.log(typeof reg);  // 正则表达式也是对象

        function fn() {

        }

        fn.name = "xiaowang";
        fn.age = 30;
        console.log(fn.age);
        console.log(typeof fn); // 值是function 但函数也是对象
    </script>
</body>
</html>
```


    2 基本数据类型与引用数据类型区别

        基本数据类型 number null undefined string boolean
        基本数据类型不能添加属性 不能拿到属性值

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
        // 基本数据类型都不能添加属性、方法
        var str = "我爱javascript";
        str.name = "lily";
        console.log(str.name); // undefined 不能访问属性说明不是对象
        console.log(typeof str); // string

        var a = null; // 空引用
        a.sex = "M";
        alert(a.sex);
    </script>
</body>
</html>
```


    3 json与js狭义对象区别

        var p1 = {
            "name":"along",
            "age":31
        }  

     json的属性必须加双引号,一般狭义对象不加引号的（特殊符号或者中文等必须加双引号，如下实例）  


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
        var obj = {
            "~~": "2019",
            "国籍": "china",
            "2018": 2018
        }  
        // 访问只能用枚举的方式，不能直接(obj.~~)这样访问
        console.log(obj["~~"]);  
    </script>
</body>

</html>
```

    