原生实现红绿灯效果

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
            width: 100px;
            height: 279px;
            background: url("images/deng.jpg");
        }
    </style>
</head>
<body>
    <div id="box1"></div>
    <div id="box2"></div>
    <script>
        var box1 = document.getElementById("box1");
        var singel = 0;  // 定义一个变量等于0表示红灯、1黄、2绿
        box1.onclick = function() {
            // 点击图片后singel就自增1循环
            singel++;
            if(singel > 2) {
                // 当变成绿灯后，再重置继续循环
                singel = 0;
            }
            box1.style.backgroundPosition = -100*singel + "px 0px";
        }

        // 这种方式要定义多个红绿灯需要再次复制一份代码，造成代码冗余
        var box2 = document.getElementById("box2");
        var singel2 = 0;
        // 0 0  -100 0  -200 0 0 0 -100 0
        box2.onclick = function() {
            singel2++;
            if (singel2>2) {
                singel2 = 0;
            }    
            box2.style.backgroundPosition = -100*singel2+"px 0px";
        }
    </script>
</body>
</html>
```

面向对象实现红绿灯

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
            width: 100px;
            height: 279px;
            background: url("images/deng.jpg");
        }
    </style>
</head>
<body>
    <script>
       // 定义一个构造函数
       function TrafficLine() {
           // 定义一个属性指向dom放div元素
           this.dom = document.createElement("div");
           // 追加到body
           document.body.appendChild(this.dom);
           // 定义一个变量控制哪个灯
           this.singel = 0;
       }

       // new一个对象
       new TrafficLine();
    </script>
</body>
</html>
```

    上面的代码构造函数里创建元素、绑定事件都写入显得比较乱不好维护
    需要将初始化追加元素，绑定事件函数，定义在构造函数外面如下所示

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
            width: 100px;
            height: 279px;
            background: url("images/deng.jpg");
        }
    </style>
</head>
<body>
    <script>
       // 定义一个构造函数
       function TrafficLine() {
           // 定义一个属性指向dom放div元素
           this.dom = null;
           this.singel = 0;
           // 外面定义个初始化函数，然后在这里调用
           // 没有这个方法，所以需要定义在原型链上，然后实例就可以调用这个方法
           this.init(); 
           this.bindEvent(); // 方法定义在原型链上实例就可以在这里调用
       }

       // 原型链上定义函数完成初始化
       TrafficLine.prototype.init = function() {
           this.dom = document.createElement("div");
           document.body.appendChild(this.dom);
       }

        // 这个原型方法是上面的对象调用的
       TrafficLine.prototype.bindEvent = function() {
           var _self = this; // 这里的this表示某个红绿灯的对象,先保存起来
            // this.dom就代表上面追加的某一个div，之后谁调用bindEvent就是谁
           this.dom.onclick = function() {
               // 这里不能用this.singel++
               // 我们是想拿到红绿灯信号对象中的single，外面定义的_self就是红绿灯对象
               // 所以不能直接这样写this.single++
               // 因为里面使用的this表示的是事件源this.dom，就像之前的div.onclick事件源
               _self.singel++;
               if(_self.singel>2) {
                   _self.singel = 0;
               }
               // 这里用this而不是this.dom
               this.style.backgroundPosition = -100*_self.singel + "px 0px";
           }
       }

       // new一个对象
       new TrafficLine();
       new TrafficLine();
    </script>
</body>
</html>
```

面向对象实现小女孩行走

        下载这个js文档使用random工具 https://www.bootcdn.cn/underscore.js/
        http://underscorejs.org/#random

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
    <style>
        div {
            width: 79px;
            height: 108px;
            background: url(images/aisidier.png) 0px -216px;
        }
    </style>
<body>
    <!-- 引入underscore-min.js使用random获取随机整数 -->
    <!-- <script src="https://D:/Git-rep/test/min.js"></script> -->
    <!-- <script src="https://cdn.bootcss.com/underscore.js/1.9.1/underscore-min.js"></script> -->
    <script>
        function Girl() {
            // 定义个dom元素放图片
            this.dom = null;
            // 定义个值表示每张图片数值
            this.singel = 0;
            // 定义小女孩的初始水平位置
            this.x = 0;
            // 小女孩垂直位置 1-500
            this.y = parseInt(Math.random()*500+1); // 获取1-500随机整数   _.random(1,10);
            // 定义行走速度
            this.speed = parseInt(Math.random()*10+1); // 获取1-10随机整数  _.random(1,10);
            this.init();
            // 把数组push到构造函数中
            array.push(this);
        }

        Girl.prototype.init = function() {
            this.dom = document.createElement("div");
            document.body.appendChild(this.dom);
        }

        Girl.prototype.update = function() {
            this.x += this.speed;
            this.singel++;
            if(this.singel>7) {
                this.singel = 0;
            }

            this.dom.style.left = this.x + "px";
            this.dom.style.top = this.y + "px";
            // -79*1px  -216px表示第一张图片
            this.dom.style.backgroundPosition = -79*this.singel+"px -216px";
        }
        
        /*
        g1 = new Girl();
        g2 = new Girl();
        */
        // 定义一个数组存放多个Girl
        var array = [];
        for(var i=0; i<20; i++) {
            // 每次new对象都会调用构造函数，所以需要将数组放到构造函数中
            new Girl();
        }
        setInterval(function() {
            for(var i=0; i<array.length; i++) {
                array[i].update();
            }
        },100)

        
    </script>
</body>
</html>
```

    优化上面的例子，点击小女孩停止行动，再次点击行走

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
    <style>
        div {
            width: 79px;
            height: 108px;
            background: url(images/aisidier.png) 0px -216px;
        }
    </style>
<body>
    <!-- 引入underscore-min.js使用random获取随机整数 -->
    <!-- <script src="https://D:/Git-rep/test/min.js"></script> -->
    <!-- <script src="https://cdn.bootcss.com/underscore.js/1.9.1/underscore-min.js"></script> -->
    <script>
        function Girl() {
            // 定义个dom元素放图片
            this.dom = null;
            // 定义个值表示每张图片数值
            this.singel = 0;
            // 定义小女孩的初始水平位置
            this.x = 0;
            // 小女孩垂直位置 1-500
            this.y = parseInt(Math.random()*500+1); // 获取1-500随机整数   _.random(1,10);
            // 定义行走速度
            this.speed = parseInt(Math.random()*10+1); // 获取1-10随机整数  _.random(1,10);
            this.init();
            // 对dom元素进行监听绑定事件
            this.bindEvent();
            // 每个小女孩需要自己控制定时器，所以在初始化才开启定时器   
            this.timer = null;
            // 添加一个属性表示运动状态：暂停还是行动
            this.isMove = true; // 默认一开始运动是true;
        }

        Girl.prototype.init = function() {
            this.dom = document.createElement("div");
            document.body.appendChild(this.dom);
            // 先将外面的this保存起来
            var _this = this;
            this.timer = setInterval(function() {
                // 不能这样this.update()调用，因为定时器的this表示window
                if (_this.isMove) {
                    _this.update();
                }
            },100);
        }

        Girl.prototype.update = function() {
            this.x += this.speed;
            this.singel++;
            if(this.singel>7) {
                this.singel = 0;
        }
            this.dom.style.left = this.x + "px";
            this.dom.style.top = this.y + "px";
            // -79*1px  -216px表示第一张图片
            this.dom.style.backgroundPosition = -79*this.singel+"px -216px";
        }

        Girl.prototype.bindEvent = function() {
            var _this = this;
            this.dom.onclick = function() {
                if(_this.isMove) {
                    clearInterval(_this.timer);
                    _this.isMove = false;
                } else {
                    _this.timer = setInterval(function() {
                        _this.update();
                    },100);
                    _this.isMove = true;
                }
                    
            }
        }
        
        /*
        g1 = new Girl();
        g2 = new Girl();
        */
        for(var i=0; i<20; i++) {
            // 每次new对象都会调用构造函数，所以需要将数组放到构造函数中
            new Girl();
        }

        // 定时器不能放在全局了，不然点击某个图片所有图片都会停止
    </script>
</body>
</html>
```

    小女孩跨过终点就消失

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
    <style>
        div {
            width: 79px;
            height: 108px;
            background: url(images/aisidier.png) 0px -216px;
        }

        hr {
            width: 1px;
            height: 860px;
            position: absolute;
            left: 1000px;
            background: skyblue;
        }
    </style>
<body>
    <hr>
    <!-- 引入underscore-min.js使用random获取随机整数 -->
    <!-- <script src="https://D:/Git-rep/test/min.js"></script> -->
    <!-- <script src="https://cdn.bootcss.com/underscore.js/1.9.1/underscore-min.js"></script> -->
    <script>
        function Girl() {
            // 定义个dom元素放图片
            this.dom = null;
            // 定义个值表示每张图片数值
            this.singel = 0;
            // 定义小女孩的初始水平位置
            this.x = 0;
            // 小女孩垂直位置 1-500
            this.y = parseInt(Math.random()*500+1); // 获取1-500随机整数   _.random(1,10);
            // 定义行走速度
            this.speed = parseInt(Math.random()*10+1); // 获取1-10随机整数  _.random(1,10);
            this.init();
            // 对dom元素进行监听绑定事件
            this.bindEvent();
            // 每个小女孩需要自己控制定时器，所以在初始化才开启定时器   
            this.timer = null;
            // 添加一个属性表示运动状态：暂停还是行动
            this.isMove = true; // 默认一开始运动是true;
        }

        Girl.prototype.init = function() {
            this.dom = document.createElement("div");
            document.body.appendChild(this.dom);
            // 先将外面的this保存起来
            var _this = this;
            this.timer = setInterval(function() {
                // 不能这样this.update()调用，因为定时器的this表示window
                if (_this.isMove) {
                    _this.update();
                }
            },100);
        }

        Girl.prototype.update = function() {
            this.x += this.speed;
            // 判断是否过线
            if (this.x>1000) {
                // 小女孩隐藏
                this.release();
            }   
            this.singel++;
            if(this.singel>7) {
                this.singel = 0;
        }
            this.dom.style.left = this.x + "px";
            this.dom.style.top = this.y + "px";
            // -79*1px  -216px表示第一张图片
            this.dom.style.backgroundPosition = -79*this.singel+"px -216px";
        }

        // 消灭女孩
        Girl.prototype.release = function() {
            document.body.removeChild(this.dom);
        }

        Girl.prototype.bindEvent = function() {
            var _this = this;
            this.dom.onclick = function() {
                if(_this.isMove) {
                    clearInterval(_this.timer);
                    _this.isMove = false;
                } else {
                    _this.timer = setInterval(function() {
                        _this.update();
                    },100);
                    _this.isMove = true;
                }
                    
            }
        }
        
        /*
        g1 = new Girl();
        g2 = new Girl();
        */
        for(var i=0; i<20; i++) {
            // 每次new对象都会调用构造函数，所以需要将数组放到构造函数中
            new Girl();
        }

        // 定时器不能放在全局了，不然点击某个图片所有图片都会停止
    </script>
</body>
</html>
```

    打气球实例

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
            width: 231.25px;
            height: 300.7px;
            background: url(star/ball.png);
            position: absolute;
        }
    </style>
</head>
<body>
    <h1 id="info"></h1>
    <h2 id="e"></h2>
    <script src="https://cdn.bootcss.com/underscore.js/1.9.1/underscore-min.js"></script>
    <script>
        var allTime = 20;
        var allScore = 0;
        function Ballon() {
            this.dom = null;
            this.x = _.random(0,document.documentElement.clientWidth - 236);
            this.y = document.documentElement.clientHeight;
            this.score = _.random(1,12);
            this.init();
            this.bindEvent();
            array.push(this);
        }

        Ballon.prototype.init = function() {
            this.dom = document.createElement("div");
            document.body.appendChild(this.dom);
            // 设置dom元素的位置
            this.dom.style.left = this.x + "px";
            this.dom.style.top = this.y + "px";
            // 设置div的backgroundPosition
            this.dom.style.backgroundPosition = -((this.score-1)%4)*231.25 + "px " +(-parseInt((this.score-1)/4)*300.7) +"px";

            //    -231.25 0     
            // 1   2    3   4       (this.score-1)%4*231.25
            // 5   6    7   8       -300.7*1  parseInt((this.score-1)/4)
            // 9   10   11  12      -300.7*2 
        }

        Ballon.prototype.move = function() {
            this.y -= this.score;
            this.dom.style.top = this.y + "px";
        }

        Ballon.prototype.bindEvent = function() {
            var _this = this;
            this.dom.onmousedown = function() {
                allScore += _this.score; 
                _this.goDie();
            }
        }

        Ballon.prototype.goDie = function() {
            document.body.removeChild(this.dom);
            for(var i=0; i<array.length; i++) {
                if (array[i] === this) {
                    array.splice(i,1);
                }
            }
        }

        var array = [];
        var frame = 0;
        var timer = setInterval(function() {
            frame++;
            if (frame%100==0) {
                allTime--;
            }
            if (allTime==0) {
                alert("游戏结束");
                clearInterval(timer);
            }
            if(frame%10==0) {
                new Ballon();
            } 
            document.getElementById("info").innerHTML = allScore;  
            _.each(array,function(item) {
                item.move();
            })
        },10);
    </script>
</body>
</html>
```

    小球碰撞

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        .box {
            width: 500px;
            height: 500px;
            border: 1px solid #f40;
            margin: 0 auto;
            position: relative;
        }

        .box p {
            position: absolute;
            background: red;
            border-radius: 50%;
        }
    </style>
</head>
<body>
    <div class="box">
    </div>
    <script src="https://cdn.bootcss.com/underscore.js/1.9.1/underscore-min.js"></script>
    <script>
        function Ballon() {
            this.dom = null;
            // 半径
            this.r = 20;
            // 圆心位置
            this.x = _.random(this.r,500-this.r);
            this.y = _.random(this.r,500-this.r);
            // this.dx  this.dy 确保球运动 dx与dy不能同时为0
            do {
                this.dx = _.random(-5,5);// [-5,5]随机整数
                this.dy = _.random(-5,5);
            }while(this.dx==0&&this.dy==0);
            console.log(this.dx,this.dy);
            this.init();
            arr.push(this);
        }

        Ballon.prototype.init = function() {
            this.dom = document.createElement("p");
            document.querySelector(".box").appendChild(this.dom);
            this.dom.style.width = (2*this.r) + "px";
            this.dom.style.height = (2*this.r) + "px";
            this.dom.style.left = (this.x-this.r) + "px";
            this.dom.style.top = (this.y-this.r) + "px";
        }

        Ballon.prototype.move = function() {
            this.x += this.dx;
            this.y += this.dy;
            if (this.x-this.r<0 || this.x+this.r>500) {
                this.dx = -this.dx;
            } else if(this.y-this.r<0 || this.y+this.r>500) {
                this.dy = -this.dy;
            }
            this.dom.style.left = (this.x-this.r) + "px";
            this.dom.style.top = (this.y-this.r) + "px";
        }
        var arr = [];
        new Ballon();
        new Ballon();
        new Ballon();
        new Ballon();
        new Ballon();
        new Ballon();
        setInterval(function() {
            // 让所有的圆球运动
            _.each(arr,function(item) {
                item.move();
            })
        },10);
    </script>
</body>
</html>
```

    内置构造函数

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
            name: "lily",
            age: 20,
            sex: "女"
        };
        console.log(obj); // Object的实例
        console.log(Object.prototype===obj.__proto__);// true
        /*
        var obj2 = new Object();
        obj2.name = "lily";
        obj2.age = 20;
        obj2.sex = "女";
        console.log(obj2);
        */

        /*          prototype
            Object--------------Object.prototype
             |                          |
             | new                      | 
             |                          |
            obj ------------------------
                       __proto__     
        */

        /* 内置构造函数Function
        function fn() {
            console.log(1); 
        }
        fn();
        // fn函数是Function实例
        console.log(fn.__proto__ === Function.prototype);
        */
        var fn = new Function("a","b","console.log(a+b)");
        fn(1,4);
        console.log(fn.__proto__ === Function.prototype);
        
        
    </script>
</body>
</html>
```





