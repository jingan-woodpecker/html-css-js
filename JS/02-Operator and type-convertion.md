一、运算符

    + 数字转换成字符串：先将数字转换成字符串，再和其它字符串进行拼接
    123+"10" 先把123变成"123",然后与"10"拼接成"12310"
      123+"" ----->"123"
      
    - "123"-10得到110   "123a"-10得到NaN，但NaN也是一种number类型  
    
    "3"-"4" 得到-1 字符串  
    
    "12" * 4得到48
    字符串转换成数字
        Number()  parseInt()  parseFloat()
        
```html
	<script type="text/javascript">
		var a = 123;
		var b = "10";
		c = a + b ;
		alert(typeof c);
		document.write("3"-false);//结果为 3，false转为0
		console.log("20"+2-"6"); //"20"+2---->"202"  结果为196
	</script>
```

二、用户输入

    prompt()为一个输入框，用户可以自定义输入内容。
    
```html
    <script type="text/javascript">
 	var num = prompt("请输入三位数");
 	var bai, shi, ge ;
 	
 	bai = parseInt(num/100);
 	shi = parseInt(num/10)%10;
 	ge = num%10;
 	
 	alert("百位数是:"+bai+";十位数是:"+shi+";个位数是:"+ge);
	</script>
```

三、自增自减

    i++与++i比较 无论什么情况最后i都会增加1,区别就是i++参与运算时采用的是i一开始值，++i参与运算采用的是i加1后的值
        i++ 或 i--  是先将i的值赋值给变量，再自增或自减1；
        ++i 或 --i  是先自增或自减1，再赋值给变量；
        
```html
<script type="text/javascript">
	var j = 7;
	var i;
	i = j++;

	alert(i+":"+j);//8:7

	var j = 7;
	var i;
	i = ++j;

	alert(i+":"+j);//8:8
</script>
```

四、关系运算符

    关系运算符组成的关系表达式结果是一个布尔值 true 成立 false不成立
    
```html
<script type="text/javascript">
	console.log(10 > 9);
	console.log(10 < 9);
	console.log(100 >= 74);
	console.log(24 <= 34);
	console.log("10" > "9");//false 字符串数字比较，一个个字符对比，1<9,所以false
	console.log("xikl" < "xili");//true 按字母排序顺序一个个比较，排序靠后的较大
	console.log("67" > 24);//true 纯数字字符串会隐式转换成数字比较
	console.log(10 == 10);//true 不严格相等，只要内容相等就相等即"10"==10
	console.log("10" == 10);//true 
	console.log(10 === "10");// false 严格相等，内容和类型都要相等
	console.log(8 != 8); //false  !=是对==的否定
	console.log("5"!=5); // false 
	console.log(10 !== 10); //false !==是对===的否定
	console.log("5"!==5); // true 
</script>
```

五、逻辑运算符

    && || !
    * && 并且 左右两个表达式全是true结果才是true，其他情况全是false
    * || 或 只要有一个表达式为true结果就是true
    * 表达式为true加!后边false
    
```html
<script type="text/javascript">
	console.log(10 > 10 && 37 >18);
	console.log(10 == 10 && 37 >18);
	console.log(10 > 10 || 37 >18);
	console.log(!(10 == 10));
</script>
```

    短路现象
    
    逻辑&&  当第一个表达式为false,整个逻辑表达式结果确定就是false,没有必要（也不会）执行后面的表达式
    || 当第一个表达式为true(非0) 结果就是第一个 表达式的值，此时不会执行第二个表达式
    
```html
<script type="text/javascript">
	var num = 12;
	console.log(3>4 && ++num);//false
	alert(num);
	
	var digit = 10;
	console.log(10 > 10 || ++digit);
	alert(digit);
</script>
```

六、条件运算符

    表达式1?表2:表3  先执行表1，表1成立返回表2作为最终结果 否则返回表3(三目运算)
   
```html
<script type="text/javascript">
	console.log(199>200?"正确的":"错误的");
</script>
```

七、赋值运算符

```html
	<script type="text/javascript">
	    // = 赋值运算符 不是等于
	    var num = 10;
	    var num2 = 12 + 6;
	    // += -= *= /= %=  复合运算符
	    num += 1;// num = num + 1; num++; ++num
	    console.log(num);
	</script>
```

八、类型转换

    * parseInt()
    
```html
<script type="text/javascript">
	console.log(parseInt("123"));//123
	console.log(parseInt("123.8999"));//123
	// 从左到右直到遇到第一个非数字字符为止,把第一个非数字字符前面的保留下来
	console.log(parseInt("12df3.99"));//12
	console.log(parseInt("123.99dd99"));//123	
</script>
```

    *parseFloat()
    
```html
<script type="text/javascript">
	console.log(parseFloat("123.333"));//123.333
	console.log(parseFloat("ddd233.34"));//NaN
	console.log(parseFloat("23kk3.45")); //23
	console.log(parseFloat("45.66kk56"));//45.66
</script>
```

    *  Number() 把其它类型转换为数字
```html
<script type="text/javascript">
	console.log(Number("384.84")) //383.84
	console.log(Number(true)) //1
	console.log(Number(false)) //0
	// Number必须要求字符串是纯数字的字符串，假如含有其他非数字或非小数点的字符则统一结果是NaN
	console.log(Number("dkj5465")) //NaN
</script>
```  

    * Boolean() 把其它类型转成布尔值
    
```html
<script type="text/javascript">
	// Boolean() 把其他类型转成布尔值
	 alert(Boolean("")); // false
     alert(Boolean("1245")); // true
     alert(Boolean(123));// true 非0数字转true
     alert(Boolean(0)); // false 
</script>
```  

    * 以某种进制输出 toString()

```html
<script type="text/javascript">
	var num = 42;
	var get_num = num.toString(2);
	alert(get_num);
</script>
```