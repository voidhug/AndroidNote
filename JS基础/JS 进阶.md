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




