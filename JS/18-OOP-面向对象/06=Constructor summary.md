构造函数总结

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
        // 自定义构造函数或类
        function People(name,age,sex) {
            this.name = name;
            this.age = age;
            this.sex = sex
        }

        var res = new People("zs",20,"男"); //拿到一个对象
        var lisi = new People("lisi",23,"女"); // new出来的对象叫People实例
        console.log(res);

        /*
            怎么看待构造函数？
            People就是一个函数 new是它的一种调用方式 不同的调用方式 函数中
            的this不一样，new的时候会调用函数 并且会创建一个对象 构造函数执行完毕
            后会返回一个对象
        
        */
    </script>
</body>
</html>
```

构造器

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
        /* 任何函数都有原型 普通函数原型没什么用
        function fun() {
            alert("hehe");  
        }
        console.log(typeof fun.prototype);
        */
        function People(name) {
            this.name = name;
        }
        console.log(People.prototype);//{constructor: ƒ}
        People.prototype = {
            constructor: People,
            name: "kaola",
            sex: "nan",
            say: function() {
                alert("yaya");
            }
        };
        console.log(People.prototype);
        // new出一个对象 不仅仅执行构造函数的语句 同时也会把这个对象的__proto__属性指向了构造函数的prototype
        var xh = new People("xiaohong");
        var xm = new People("xiaoming");
        console.log(xh.name); // "xiaohong"
        console.log(xh.age);
        console.log(xh.__proto__ === xm.__proto__);
        xh.say();
        xm.say();
    </script>
</body>
</html>
```

构造函数属性

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
        function Dog() {

        }
        console.log(Dog.prototype.constructor);
        console.log(new Dog().constructor);

        /*     prototype  
           Dog-------------->Dog.protoype
              <--------------
                 constructor
        */
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
        function Cat() {

        }
        // Cat.prototype
        var xiaohua = new Cat();
        console.log(xiaohua.__proto__.__proto__.constructor); // Object函数
        console.log(xiaohua.__proto__.__proto__.__proto__); // null

        Object.prototype.hehe = function() {
            alert("hehe");
        }
        //xiaohua.hehe();

        var arr = [1,2,3]; // var arr = new Array(1,2,3);
        console.log(typeof arr);
        //arr.hehe();

        var str = "123"; // var str = new String("123");
        //str.hehe();

        var num = 123; // var num = new Number("123");
        num.hehe();
        /*
            Object.prototype 是所有对象的原型链终点   
            Object---------Object.prototype {hehe:}
                                ^
                prototype       |  __proto__
            Cat------------>Cat.prototype  {}
             |                  |
            xiaohua-------------
                     __proto__
        
        */

        /*
           Object---------Object.prototype {hehe:**}
                                   ^
                    prototype      |  __prto__   
           Array----------------Array.prototype 
            |                        ^
            | new                    |
           arr----------------------- 
                 __proto__
        */
    </script>
</body>
</html>
```

    定义一个方法在原型上，以后能把所有数组都调用
    
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
        function Dog() {

        }
        /*
          var Dog = new Function()   
        */
        /* 证明 函数也是对象
        Dog.aa = 123;
        alert(Dog.aa);
        */
        console.log(Dog.__proto__.constructor); // Function
        Function.prototype.pei = function() {
            console.log("pei");
        }
        Dog.pei();


        // 数组
        var arr = [1,2,78,34,5]; // new Array()
        var arr2 = [1,2,3,4,5];
        // 增加方法 以后能把所有数组调用
        Array.prototype.max = function() {
            var max = this[0];
            for(var i=1; i<this.length; i++) {
                if (this[i]>max) {
                    max = this[i];
                }
            }
            return max;
        }
        alert(arr.max());
        alert(arr2.max());

    </script>
</body>
</html>
```