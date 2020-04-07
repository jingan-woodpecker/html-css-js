window对象

    （1）可在控制台输入：window 就会显示大部分对象
    例如：window.alert("ok"),其中window可以省略

![window](picture/window1.png)

    （2）定义的全局变量会挂载到window的对象下
    （3）定义的全局函数同样也会

```html
<script>
    var d = 100;
    alert(d);
    // alert(window.d) 跟上面的效果一致

    function fn() {
        alert(3);
    }
    fn()
    // window.fn() 跟上面效果一致
</script>
```
![windows2](picture/window2.png)

