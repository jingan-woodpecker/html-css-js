```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	
	<script type="text/javascript">
	    // 1 计算数组中所有偶数的和和奇数的和 并且统计偶数和奇数个数

	    function getCount(arr) {
            var oddSum = 0;  // 记住奇数的和
            var oddCount = 0;// 统计奇数个数 
            for(var i=0, len=arr.length; i<len; i++) {
            	if (arr[i]%2) {
            		oddSum += arr[i];
            		oddCount++;
            	}
            }
            console.log("所有奇数之和"+oddSum);
            console.log("所有奇数个数"+oddCount);
	    }

	    var arr = [12,4,5,7,11,2,3];
	    getCount(arr);

	    // 2 输出数组中最大值和最小值
	    function getValue(arr) {
           // 定义一个数组 存最大值和最小值
           var res = [];
           var max = arr[0];// 默认值
           var min = arr[0];
           for(var i=1, len=arr.length; i<len; i++) {
           	    if (arr[i]>max) {
           	    	max = arr[i];
           	    }
           	    if(arr[i]<min) {
           	    	min = arr[i];
           	    }
           }
           res[0] = max;
           res[1] = min;
           return res;
	    }

	    var arr = [-1,10,2,-5,19];
	    var res = getValue(arr);
	    console.log(res);
        
	</script>
</body>
</html>
```