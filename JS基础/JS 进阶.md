JavaScript 进阶
===
```JavaScript
// JavaScript 是若类型语言，pages 即可以是数组，也可以是一个 PageLayoutObject。
var pages = [];
pages = new UI.PageLayoutObject(pages); // 先执行 new，再赋值。
```
```JavaScript
btn.RegisterEvent("Click", (function (_idx) {
	return function () {
 		pages.AccessActivePage(_idx);
 		// 外层有个 for 循环，当循环到 i 的时候，就把这个 i 给传入，立即执行外层 function，返回内层 function。必须要等到 btn 被点击的时候，function 才会被执行，**JavaScript 是按照执行的先后顺序来执行代码。**
 	}
})(i)); 
```
获取时间戳，从 1970 年 1 月 1 日 午夜开始计算的毫秒数。

```JavaScript
var time = new Date().getTime();
var time = Date.parse(new Date());
var time = (new Date()).valueOf(); // 精确到秒，毫秒显示为0。
```

call 后面跟参数列表
apply 后面跟对象和参数列表

清空数组

```JavaScipt
// 方法一
var ary = [1, 2, 3, 4];
ary.splice(0, ary.length);

// 方法二
var ary = [1, 2, 3, 4];
ary.length = 0; // 可对 length 进行写操作，Java 只可以读。

// 方法三
var ary = [1, 2, 3, 4];
ary = [];

// 我测了以下，都是 0 ms。
var a = [];
for (var i = 0; i < 1000000; i++) {
	a.push(i);
}
var start = new Date().getTime();
a.length = 0;
// a = [];
var end = new Date().getTime();
alert(end - start);
```

jQuery 使用 Ajax
点击 save，然后就发 ajax 了，有 type、url、data、dataType、success、error；
success 也有错误，success 的错误是 data 的错误，error 是 jqXHR 的错误。==什么叫 data 的错误？什么叫 error 的错误？==
最好的方法是看源码。

```JavaScript
$("#save").click(function(){ 
	$.ajax({ 
	    type: "POST", 	
		url: "serverjson.php",
		data: {
			name: $("#staffName").val(), 
			number: $("#staffNumber").val(), 
			sex: $("#staffSex").val(), 
			job: $("#staffJob").val()
		},
		dataType: "json",
		success: function(data){
			if (data.success) { 
				$("#createResult").html(data.msg);
			} else {
				$("#createResult").html("出现错误：" + data.msg);
			}  
		},
		error: function(jqXHR){     
		   alert("发生错误：" + jqXHR.status);  
		},     
	});
});
```



