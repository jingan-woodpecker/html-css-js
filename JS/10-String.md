```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	
	<script type="text/javascript">
	    // 字符串  由单引号或双引号引起的一组字符序列
	    var str = "hello";
	    var str2 = '我们';
	    // 字符串相关api
	    /*
	       charAt(n)     返回索引号位置n上的字符
	       charCodeAt(n) 返回位置n上的字符的unicode编码
	                'a'   97    
	                'A'   65
	                '0'   48  
	       String.fromCharCode(65); // 返回数字对应的字符         
		
	    var ch = str.charAt(2);
	    var ch_num = str.charCodeAt(1);
	    var res = String.fromCharCode(65); // 返回数字对应的字符
	    //alert(ch); // h
	    //alert(ch_num); // 104  
	    alert(res);
	    */

	    /*
           indexOf("字符")  从左到右在字符串中查到第一个符合的字符,找到就返回该位置，找不到返回-1 
           lastIndexOf("o") 基本同上 只不过从后往前查找
	    var str = "how do you do?";
	    var index = str.indexOf("o",2);
	    var lastIndex = str.lastIndexOf("o");
	    var index_error = str.indexOf("z");
	    alert(index); // 1
	    //alert(index_error); // -1
	    */

	    /*
	      substr(num) 表示字符串从num这个位置一直截取到最后,原来字符串不变
	      substr(num,length)
	      表示字符串从num这个位置截取length长度的字符串 
	      substring(num)
	      表示字符串从num这个位置一直截取到最后,原来字符串不变
	      substring(from,to)
	      表示字符串从from位置开始 截取到to这个位置 但是不包含to这个位置
	      思考：
	             "afkqz" 向字符串加一个m 保证原来顺序不变 "afkmqz" 
	    
	    var str = "welcome to china";
	    //var res1 = str.substr(2);
	    var res1 = str.substr(2,3);
	    console.log(res1);// "lcome to china"
	    console.log(str);
	    //var str2 = str.substring(2);
	    var str2 = str.substring(2,6); // lcom
	    console.log(str2);// lcome to china
	    */

	    /* split() 把字符串分割成字符串数组
	    var str = "My name is along";
	    var res = str.split(" ");
	    console.log(res);// ["My", "name", "is", "along"]
	    var arr = ["My", "name", "is", "along"];
	    // var res_str = arr.join(" ");
	    // console.log(res_str);
	    */
	    // 拿到网址字符串的uname和psw
	    var url = "http://www.baidu.com?uname=zs&psw=123456";
	    var arr = url.split("?");
	    arr = arr[1].split("&"); // ["uname=zs","psw=123456"]
	    var uname = arr[0].split("=")[1];
	    var psw = arr[1].split("=")[1];
        console.log(uname,psw);  

        // "lmnopq" 按照"qponml"
        var str = "lmnopq";
        var arr = str.split("");
        var res = arr.reverse().join("");
        console.log(res); // qponml      
	</script>
	</script>
</body>
</html>
```