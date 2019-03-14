```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
	   // 排序 
	   var arr = [10,4,12,-2];
	   function bubbleSort(arr) {
	   	   	// 定义一个循环 控制轮数  arr.length-1 
	   		for(var i=0; i<arr.length-1; i++) {
	   	  		// 定义一个循环 控制每相邻两个数比较
	   	  		for(j=0; j<=arr.length-2-i ;j++) {
	   	  			if (arr[j] > arr[j+1]) {
	   	  				var temp = arr[j];
	   	  				arr[j] = arr[j+1];
	   	  				arr[j+1] = temp;
	   	  			}
	   	  		}
	      }
	   }  
	   bubbleSort(arr);
	   alert(arr);
	</script>
</body>
</html>
```

数组已经排序完成了，但是按上面的代码来看，数组还会继续排序，所以我们加一个标志位，如果某次循环完后，没有任何两数进行交换，就将标志位 设置为 true，表示排序完成，这样我们就可以减少不必要的排序，提高性能。

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript">
         function bubble(arr4) {
             var len = arr4.length-1;
             for(i=0; i<len; i++) {
                var flag = true;
                for(j=0; j<len-i; j++) {
                    if(arr4[j]>arr4[j+1]) {
                        var temp = arr4[j];
                        arr4[j] = arr4[j+1];
                        arr4[j+1] = temp;
                        flag = false;
                    }
                }
                if(flag) {
                    break;
                }
             }
             return arr4;
         }

         var bubbleNum = [22,334,55,677,11,-1];
         var res3 = bubble(bubbleNum);
         console.log(res3); 
	</script>
</body>
</html>
```
