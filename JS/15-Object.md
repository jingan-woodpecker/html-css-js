基本数据类型

    Number String Boolean null undefined

引用数据类型

    Object Array Date Function 正则表达式
    函数和数组都是对象

对象(属性:属性值)

    由无序的属性集合组成{k:v,k:v,k:v}
    属性值不仅有信息还有行为，行为对于程序来说就是方法或者函数    

    对象直接量
    var list = {
        "name":"lisi",
        "age":22,
        "sex":"男"
    }

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
        // 描述一个用户信息，用定义参数值和对象的方式存储对比
        var name = "lisi";
        var age = "29";
        var sex = "男";

        // 用对象描述张三，对象是一个整体
        var zs = {
            name: "zhangsan", // 属性  属性名：属性值
            age: "20",
            sex: "女",
            // 行为（函数或者方法）
            study: function() {
                alert("great!");
            },
            eat: function() {
                alert("吃货");
            }
        }
    </script>
</body>
</html>
```


    对象的成员访问：对象.成员
    动态添加属性以及行为

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
        // 描述一个用户信息，用定义参数值和对象的方式存储对比
        var name = "lisi";
        var age = "29";
        var sex = "男";

        // 用对象描述张三，对象是一个整体
        var zs = {
            name: "zhangsan", // 属性  属性名：属性值
            age: "20",
            sex: "女",
            // 行为（函数或者方法）
            study: function() {
                alert("great!");
            },
            eat: function() {
                alert("吃货");
            }
        }

        // 对象成员的访问：对象.成员
        console.log(zs.name);
        console.log(zs.sex);
        // 注意调用对象的方法加括号，还有不可以单独写成study(),不然会默认全局查找window.study()
        console.log(zs.study());

        // 因为随着时间推移，信息可能有所补充，所以就会出现动态添加属性
        zs.issingel = false;
        alert(zs.issingel);

        // 动态添加行为
        zs.coding = function() {
            alert("动态添加行为");
        }
        zs.coding();
    </script>
</body>
</html>
```

JS基本类型和对象类型（JS中可以一切看做对象）

    基本类型不支持添加属性

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
        // 基本类型不能动态添加属性
        var num = 10;
        num.index = 111;
        alert(num.index);  // undefined
    </script>
</body>
</html>
```

值的赋值和对象赋值不同之处

    对象赋值指的是地址的赋值：比如一个人先去图书馆借书，然后撕了一张纸，后面
    一个同学也去借同一本书，那这本书也是被撕了的，是同一本书；
    相比对象赋值也是，修改的也是同一个地址

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
        // 值的赋值
        var i = 10;
        var j = i;
        i = 19;
        alert(i);  //10

        // 对象的赋值
        // 对象存储的值在堆内存里，占用了一块空间，内存有个地址，对象的赋值obj={name:"zs"}
        // 是说把这个地址赋值了，所以obj存储的是对象的地址，然后obj赋值给obj1,这样两个都指
        // 向同一个对象，所以修改对象为obj1.name = "lisi"，修改的同一个地址，所以obj和obj1都为lisi  
        var obj = {name:"zs"};
        var obj1 = obj;
        obj1.name = "lisi";
        alert(obj.name);  //lisi

        var arr = [3,5,6];
        var brr = arr;
        arr[0] = 8;
        alert(brr); // arr和brr都是[8,5,6]

    </script>
</body>
</html>
```

数据交换格式json




