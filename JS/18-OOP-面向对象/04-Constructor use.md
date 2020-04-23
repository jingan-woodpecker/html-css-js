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
        // 定义一个构造函数（类）
        function People() {
            this.name = "lisi",
            this.age = 23
        }
        
        // new一个对象，赋值给res，这个res就叫（实例对象）
        var res = new People();
        // 打印实例
        console.log(res);
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
        function A() {
            this.m = 10;
        }

        function B() {
            this.m = 20;
        }

        // 相当于调用A函数并把this指向改为B即B.m = 10
        // (函数.m)可以用这种格式原因：函数也是一种对象，所以可以添加属性
        A.call(B); 
        // 同理调用B且改变指向所以A.m = 20
        B.call(A);

        // new一个对象四部曲：{},然后this指向这个对象，所以{m:10}，执行后返回到A
        var a = new A(); 
        // {m:20}
        var b = new B(); 
        console.log(a.m == B.m); // true
        console.log(b.m == A.m); // true
    </script>
</body>
</html>
```