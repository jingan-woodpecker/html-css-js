```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	
	<script type="text/javascript">
	   // api application interface 应用程序接口
	   // 数组的增加与删除
	   /* push()    在数组的末尾添加一个或多个元素
          unshift()  .......前面。。。。。。 
          以下两个方法表示删除,它们返回值是删除的元素
          pop()     在数组的末尾删除一个元素
          shift()   .......前面。。。。。 
	   */
       
       
	   var numbers = [1,2,3,4,5];
	   //numbers[5] = 6;
	   //numbers[numbers.length] = 6;
	   numbers.push(6);
	   numbers.push(7,8);
	   numbers.unshift(-1,0);
	   console.log(numbers);
        
	   /*
            1 2 3  ------>  0  1 2 3
	   */
	   
	   var arr = [1,2,3];
	   for(var i=arr.length; i>=1; i--) {
	   	     arr[i] = arr[i-1];
	   }
	   arr[0] = 0;
	   console.log(arr);
	   

	   var arr1 = [1,3,5,7,9];
	   arr1.pop(); // 9
	   arr1.pop();
	   arr1.shift();
	   console.log(arr1);


	   // 在数组任意位置删除或添加元素 splice()
	   var arr = [1,2,3,4,5,6];
	   arr.splice(3,2); // 表示从索引3开始 删除2个元素
	   arr.splice(4,1);
	   arr.splice(3,0,3.5,3.8); // 从索引为3开始 添加多个元素
	   arr.splice(3,2,3.5,3.8,3.9); // 从索引为3开始替换后两个元素，3.9依然添加到后面
	   console.log(arr); // [1,2,3,6]
	</script>		
</body>
</html>
```