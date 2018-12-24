```html
<script type="text/javascript">
    //方案一
	// 素数-质数  只能被1和自己整除的数
	// 判断一个数是否为素数
	var num = parseInt(prompt("请输入数值："));
	var bool = true;
	for(var i=2; i<num; i++) {
		if(num%i == 0) {
			bool = false;
			break;
		}
	}

	if(bool) {
		console.log(num+"：是素数");
	} else {
		console.log(num+"：不是素数");
	}
</script>
```

```html
<script type="text/javascript">
	//方案二
	var count = 0;
	var num = parseInt(prompt("请输入数值："));
	for(var i=1; i<=num; i++) {
		if(num%i === 0) {
			count++;
		}
	}

	if(count === 2) {
		console.log(num+"：是素数");
	} else {
		console.log(num+"：不是素数");
	}
</script>
```
