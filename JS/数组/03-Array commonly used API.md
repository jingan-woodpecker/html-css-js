```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	
	<script type="text/javascript">
	    // concat 表示数组连接其他值  不改变原数组
	    var arr1 = [1,2,3,4];
	    var arr2 = [5,6,7,8];
	    var res = arr2.concat(arr1,9);
	    console.log(res);

        // 迭代器方法
        function isEven(x) {
        	console.log(x);
        	return x%2===0?true:false;
        }
        var numbers = [1,2,3,4,5,6];
        // every方法会迭代数组中每个元素  直到遇到返回false
        numbers.every(isEven);

        // some基本与every行为类似,会迭代数组每个元素 直到遇到返回为true结束
        numbers.some(isEven);

         /* forEach 与for循环结果相同
         numbers.forEach(function(x) {
             console.log(x);
         });
         */

         //map
         var res1 = numbers.map(isEven);
         console.log(res1); // [false, true, false, true, false, true]
         
         // filter 返回一个新数组 新数组由函数返回true的元素组成
         var res2 = numbers.filter(isEven);
         console.log(res2); // [2, 4, 6]
         

         // reduce
         var sum = numbers.reduce(function(prev,current,index,array) {
             console.log(prev,current);
             return prev+current;
         });
         alert(sum);

         // 一开始prev代表1  current代表2
         // prev会利用上一次函数返回值
         // 1 2
         // undefined 3
         // undefined 4
         // undefined 5
         // undefined 6
         // function fn() {

         // }

         // alert(fn());
 
         // 1   2  返回3
         //   3    3 返回6
         //   6     4
         //   10      5
         //   15        6 返回21 最后一次返回值会作为整个reduce的返回值
	</script>
</body>
</html>
```