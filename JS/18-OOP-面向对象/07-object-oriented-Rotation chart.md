面向对象实现轮播图效果

    需要准备的东西
    1、多张图片
    2、下载好的：jquery-1.12.3.min.js文件
    3、创建一个js文件和一个html文件


下面为Carsouel.js文件内容

```js
// 匿名函数自执行（定义后马上执行），解决全局调用时，同名函数被覆盖
// 所以在这个自执行函数里面定义函数可以形成一个局部作用域，不会跟全局的同名函数起冲突
(function() {
    var num =10;
    function Carsouel(json) {
        // 需要创建dom元素，外层盒子
        // 查使用jquery找id元素方式固定格式是"#"+json.id，其中传入的json参数有个属性id，所以就用json.id调用
        this.$dom = $("#"+json.id);
        // ul 初始化为null
        this.$ul = null;
        // ul下的所有li,初始化为null
        this.$ulli = null;
        // 左侧切换按钮
        this.$left = null; 
        // 右侧切换按钮
        this.$right = null;
        this.$ol = null;
        this.$ollis = null;
        // 添加一个控制变量，控制显示哪张图片
        this.idx = 0;
        // 动画时间
        this.animateTime = json.animateTime; 
        // 外层盒子宽高（尽量不要把定义的东西写死）
        this.width = json.width;
        this.height = json.height;
        // 图片数组属性
        this.imgArr = json.images;
        // 图片长度
        this.imgArrLength = json.images.length;
        // 初始化
        this.init();
        // 时间监听
        this.bindEvent();
    }

    Carsouel.prototype.init = function() {
        this.$ul = $("<ul></ul>");
        // ul下循环添加Li元素和图片
        for(var i=0; i<this.imgArr.length; i++) {
            // 图片路径需要进行拼接
            this.$ul.append($(" <li><img src='"+this.imgArr[i]+"'></li>"));
        }
        // 把ul放到dom下
        this.$dom.append(this.$ul);

        // 拿到ul下所有li
        this.$ulli = this.$ul.find("li");
        // 最外层盒子设置样式
        this.$dom.css({
            // 子绝父相
            "position": "relative",
            "width": this.width,
            "height": this.height,
            "margin": "0 auto",
            "border": "1px solid gray",
            "overflow": "hidden"
        });

        // ul的css样式
        var _this = this // 相当于new出来的轮播对象
        this.$ul.css ({
            "position": "absolute",
            // 跟最外层盒子宽度一致
            "width": _this.width,
            "height": _this.height
        });

        // ul下li的css样式
        this.$ulli.css ({
            // 让所有li都绝对定位
            "position": "absolute",
            // 先让图片放一起重叠，用户点击切换才轮播，让left值等于width
            "left": _this.width
        });

        // 单独设置默认第一张图片的css样式
        this.$ulli.eq(0).css ({
            "left": 0
        });

        // 初始化左右切换按钮
        this.$left = $("<a class='left'><</a>");
        this.$right = $("<a class='right'>></a>");
        // 按钮需要作为最外层盒子的儿子，需要添加到dom中
        this.$dom.append(this.$left);
        this.$dom.append(this.$right);

        // 初始化下面ol控制列表
        this.$ol = $("<ol class='circle'></ol>");
        // ul下循环添加Li元素和图片
        for(var i=0; i<this.imgArr.length; i++) {
            // 图片路径需要进行拼接
            this.$ol.append($(" <li></li>"));
        }
        // 把ul放到dom下
        this.$dom.append(this.$ol);

        // 拿到ul下所有li
        this.$ollis = this.$ol.find("li");

        this.$ol.css ({
            "position": "absolute",
            "bottom": 10,
            "left": 400,
            "list-style": "none"
        });

        // ul下li的css样式
        this.$ollis.css ({
            // 让所有li都绝对定位
            "float": "left",
            "width": 20,
            "height": 20,
            "margin-left": 10,
        });

        // ol下的第一个li高亮显示
        this.$ollis.eq(0).addClass("active");
    }

    Carsouel.prototype.bindEvent = function() {
        // 左侧切换按钮
        var _this = this;
        this.$left.click(function() {
            // 找到具体当前的图片，然后执行动画,animate第一个参数是json，第二个参数是时间
            _this.$ulli.eq(_this.idx).animate({"left":_this.width},_this.animateTime);
            // 点击切换按钮后，图片序号++
            _this.idx++;
            // 当切换到最后一张图片时重置为0
            if(_this.idx > _this.imgArrLength-1) {
                _this.idx = 0
            }
            _this.$ulli.eq(_this.idx).css({
                "left":_this.width
            }).animate({"left":0},_this.animateTime);
        });

        // 右侧切换按钮

        // ol下li的事件绑定
        this.$ollis.click(function() {
            // 点击那个小圆点就显示那张图片
            var old = _this.idx;
            // 这个this是事件源
            var num = $(this).index();
            _this.idx = num;
            // 如果多次点击同一个圆点不做任何处理
            if(old == num) {
                return;
            }
            _this.$ulli.eq(old).css({
                "left": 0
            }).animate({"left":_this.width},_this.animateTime);

            _this.$ulli.eq(num).css({
                "left": _this.width
            }).animate({"left":0},_this.animateTime);

            // 小圆点点击后对应样式变化设置
            // 点击后当前圆点有颜色，其余清除（排他思想）
            _this.$ollis.eq(num).addClass("active").siblings().removeClass("active");
        })

    }
    window.Carsouel = Carsouel;
})();
```

下面为html文件内容

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

        .left, .right {
            top: 50%;
            width: 50px;
            height: 50px;
            line-height: 50px;
            margin-top: -25px;
            border-radius: 20%;
            text-align: center;
            position: absolute;
            background: seashell;
        }

        .right {
            right: 1px;
        }

        .circle li {
            background: #ccc;
            border-radius: 50%;
        }

        .circle li.active {
            background: slateblue;
        }
    </style>
</head>
<body>
    <div id="box"></div>
    <div class="box2"></div>
    <!-- 导入jqery库 -->
    <script src="jquery-1.12.3.min.js"></script>
    <script src="Carsouel.js"></script>
    <script>
        new Carsouel({
            "id": "box",
            "images": ["images/pic(1).jpg","images/pic(2).jpg","images/pic(3).jpg","images/pic(4).jpg"],
            // 不需要带单位
            "width": 960,
            "height": 600,
            "animateTime": 50,
        });
    </script>
</body>
</html>
```
