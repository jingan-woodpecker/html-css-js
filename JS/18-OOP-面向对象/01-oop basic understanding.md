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


    3 json与js狭义对象的比较

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

    对象中的方法

        在对象里定义函数就叫对象中的方法
        调用的两种方式如下实例：
        一、对象名.方法() ——》 xiaohong.say();
        二、定义变量接收，但是不要加小括号，否则传入的是函数的值而不是函数 ——》var fn = xiaohong.say

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
        var xiaohong = {
            name: "小红",
            age: 18,
            hobby: ["coding","eating"],
            say:function() {
                console.log("嗓子好");
            }     
         };
         xiaohong.say(); // 对象名.方法()
         var fn = xiaohong.say; //不用加小括号，加了括号表示传入函数值，不是函数
         fn();
    </script>
</body>
</html>
```

函数的上下文

    指的就是搞清楚this代表谁

    第一种：函数假如是圆括号执行 函数的上下文就是window

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
        // 判断this代表谁
        var a = 100;
        function fn(a,b,c,d,e,f) {
            var a = 200;
            // 谁调用this就是谁，这里是window调用，所以是window.a
            console.log(this.a); 
        }

        fn(1,4,5,22,53,24); // 直接函数调用，相当于window调用即：window.fn()
        // 全局定义的变量或者函数都会在window上映射，可以在控制台输入window查看下
        console.log(window);
    </script>
</body>
</html>
```

    第二种：函数作为事件处理函数，就是执行操作后才触发， 那么函数上下文就是这个事件触发的对象

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            margin-bottom: 10px;
            background-color: pink;
        }
    </style>
</head>
    <div></div>
    <div></div>
    <div></div>
<body>
    <script>
        // 封装一个函数，改变当前背景为红色
        // 事件发生后才调用这个函数，所以这个this代表的是事件源
        function changeColor() {
            this.style.background = "red";
        }

        var divs = document.querySelectorAll("div");
        for(var i=0; i<divs.length; i++) {
            // 这里注意调用changeColor不要添加括号，否则变成调用函数返回值，不是函数了
            divs[i].onclick = changeColor;
        }
    </script>
</body>
</html>
```

    第三种：函数作为对象的方法 对象打点调用 那么函数上下文是这个对象

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
        function say() {
            name = "xiaohang";
            console.log(this.name);
        }

        var obj = {
            name : "xiaojun",
            age : 28,
            sex : "女",
            say : say
        }
        
        // 谁调用this指的就是谁，这里是obj调用，所以调用的name是obj对象里的name
        obj.say(); 
    </script>
</body>
</html>
```

    第四种 定时器函数上下文是window 需要改成事件源则在定时器外面将this用变量先存储

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            background: pink;
            margin-bottom: 10px
        }
    </style>
</head>
    <div></div>
    <div></div>
    <div></div>
<body>
    <script>
        // 定时器函数上下文默认是window,想要解决这种问题且不使用div[0]这种方式
        // 因为在定时器外面的this是事件源，所以可以用一个变量先存储
        var divs = document.querySelectorAll("div");
        divs[0].onclick = function() {
            var _this = this;  // 这个this表示事件源
            setInterval (function() {
                /* 
                定时器里直接使用this是无效的,不是当前事件源，是window
                this.style.background = "green";
                可以使用divs[0].this.style.background
                */
                _this.style.background = "green";
            },1000)
            

        }
    </script>
</body>
</html>
```

    第五种：函数作为数组元素 被索引出来执行 函数上下文是这个数组

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
        function fn() {
            console.log(this.length);
        }

        arr = [fn,3,5,33,11];
        // 调用数组中的函数
        arr[0]();
    </script>
</body>
</html>
```

arguments类数组对象：本质上是对象，长的像数组

    callee 指的是函数本身

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
        function getSum(a,b,c,d,e) {
            console.log(arguments.length); // 实参个数
            // callee 指的是函数本身
            console.log(arguments.callee.length); // 形参个数
            console.log(getSum.length); // 形参个数
            console.log(typeof arguments); //arguments是对象
            console.dir(arguments) // 查看详情信息
        }

        getSum(1,2,3);
    </script>
</body>
</html>
```

应用


        预解析做的事情：变量声明提升只提升变量，赋值不提升；
        带function的声明和赋值同时提升
        
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
        /*
            下面的代码从上往下执行，先提升var a，然后提升function fn()，暂时不会提升
            fn()函数里的a,因为此时还没有调用执行，所以有如下结果

            var a;
            function fn() {
                console.log(a);
                var a = 20;
            }

            到这里预解析就结束了，代码就等价于如下这样

            var a;
            function fn() {
                console.log(a);
                var a = 20;
            }

            console.log(a);  // 变量定义了还没赋值，所以是undefined
            a = 10;
            fn(); // 调用这个函数，会形成私有作用域，执行代码前也会做变量提升，所以这个也是undefined
            console.log(a); // 这个a使用的是全局变量，所以为10  
        

        */
        console.log(a);
        var a = 10;
        function fn() {
            console.log(a);
            var a = 20;
        }

        fn();
        console.log(a);


    </script>
</body>
</html>
```

    函数上下文练习

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
        function fn() {
            alert(this.a);
        }

        var obj = {
            "a" : 1,
            "b" : 2,
            "c" : [{
                "a" : 3,
                "b" : 4,
                "c" : fn
            }]
        }

        var a = 6;
        // obj.c[0]找到这个对象，函数打点调用，谁调用就是谁
        obj.c[0].c();  //a的值等于3
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
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <script>
        function fn1(a,b,c,d,e,f,g) {
            console.log(this);
            alert(this.callee.length);
        }

        function fn2(a,b,c,d,e) {
            // arguments[fn1,3,4]  
            // 函数作为数组元素 被索引出来执行 函数上下文是这个数组
            arguments[0](3,4,2,5,3);
        }

        fn2(fn1,3,4);

    </script>
</body>
</html>
```

练习

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
        var x = 10;
        function fn(m,n,x) {
            alert(x);
            arguments[2] = 20;
            alert(x);
        }
        // 因为上面函数没有返回值，所以默认是undefined
        x = fn(1,2,3);
        alert(x);
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
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <script> 
        /*
           fun2->f
           2->a
           4->b
           6->c
           这些参数也会在arguments存储一份所以8,10在arguments中接收
           fun的arguments [fun2,2,4,6,8,10]
        
        */   
        function fun(f,a,b,c) {
            // 被数组索引出来fn2
            arguments[0](5,8);
        }

        function fun2(i,j,k,l,m) {
            // this代表函数所在的数组 fun的arguments
            alert(this.length);  // 6
            alert(this.callee.length); // 4
            alert(arguments.length);  // 2
            alert(arguments.callee.length);  // 5 形参个数
        }

        fun(fun2,2,4,6,8,10)
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
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <script> 
        var c = 100;
        var obj = {
            "a" : function() {
                return this.b;
            },
            "b" : function() {
                return this.c;
            },
            "c" : 10
        }

        var res = obj.a()();
        alert(res);
        /*
            首先obj.a()的调用，因为是对象打点调用所以this相当于obj
            返回的obj.b ==== funciton() {
                return this.c;
            }

            最后obj.b()调用就是上面的函数调用 (function() {
                return this.c;
            })()
            这种形式的调用为window.c调用，结果res = 100
        */
    </script>
</body>
</html>
```

apply和call方法

    改变函数this属性指向

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
        // this arguments都是属性  方法apply call
        // 未用apply call 方法时，this指向不会改变，所以this不等于obj
        function sum(a,b,c,d) {
            console.log(a+b+c+d); // 10
            console.log(this === obj) // false
        }

        var obj = {
            name : "xiaoli",
            age : 39,
            sex : "女"
        }

        // sum() 函数名带括号直接调用this代表window
        sum(1,2,3,4)
    </script>
</body>
</html>
```

    call方法使用

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
        // this arguments都是属性  方法apply call
        // 未用apply call 方法时，this指向不会改变
        function sum(a,b,c,d) {
            console.log(a+b+c+d); // 10
            console.log(this === obj) // true
        }

        var obj = {
            name : "xiaoli",
            age : 39,
            sex : "女"
        }
        // sum() 函数名带括号直接调用this代表window
        // call()也可以调用函数，它的参数除了接受实际参数外，第一个参数还可以代表this
        // 比如想让this和obj相等，如下调用即可,此时obj === this
        sum.call(obj,1,2,3,4)
    </script>
</body>
</html>
```

    apply基本功能与call一样 区别在于传递参数语法不一样，实参需要放在数组里面

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
        // this arguments都是属性  方法apply call
        // 未用apply call 方法时，this指向不会改变
        function sum(a,b,c,d) {
            console.log(a+b+c+d); // 10
            console.log(this === obj) // true
        }

        var obj = {
            name : "xiaoli",
            age : 39,
            sex : "女"
        }
        // sum() 函数名带括号直接调用this代表window
        // apply()也可以调用函数，基本功能与call一样 区别在于传递参数语法不一样，实参需要放在数组里面
        // 比如想让this和obj相等，如下调用即可,此时obj === this
        sum.apply(obj,[1,2,3,4])

        // Math对象中min求最小值的方法  加上window改变内部指向
        alert(Math.min.apply(window,[10,-4,11,0,9]));
    </script>
</body>
</html>
```

    







