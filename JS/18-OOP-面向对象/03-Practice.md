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
        var a = 10;
        var obj = {
            a : 2,
            add : function() {
                return this.a++;
            }
    }
    console.log(obj.add()); // 3  对象打点调用
    console.log(obj.add()); // 5
    alert(a); // 全局 10
    </script>
  
</body>
</html>
```

``html
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
        var a = 10;
        var obj = {
            a : 2,
            add : function() {
                return this.a++;
            }
    };

    var obj2 = {
            a : 2,
            add2 : obj.add
    };
    obj2.add(); // 谁调用返回谁，调用的是obj2,跟函数在哪个位置关系不大
    alert(obj2.a) // 13 

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
        function fun(fn,x,y,z) {
            // 函数作为数组元素，通过索引调用，this指的就是这个类数组arguments[fun2,11,2]
            arguments[0](); 
        }

        function fun2(a,b,c,d,e,f) {
            alert(this.length); // this指的是类数组所以arguments[fun2,11,2]长度是3
            alert(this.callee.length); // this指的是arguments[]这个数组所在函数，形参个数为4
            alert(arguments.length); // arguments这里指的是内部的长度：0
            alert(arguments.callee.length) // argument内部形参个数 6
        }

        fun(fun2,11,2);
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
        var length = 10;
        function fn() {
            alert(this.length);
        }

         var obj = {
            length: 5,
            method: function(fn) {
                alert(this===obj); // true
                fn(); // window调用fn()所以fn函数里this代表window 10
                fn.call(this); // 把fn函数的指向改变为obj 所以等于 5
                arguments[0]();// 1 [fn]
            }
        }
        obj.method(fn);
    </script>
  
</body>
</html>
```
