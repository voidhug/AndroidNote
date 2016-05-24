- 实现懒加载   
	- 需求  
		WebView 初始化，太慢。目前解决思路有两种，使用 canvas 和懒加载。先试试懒加载。
	- 思维过程  
	==瞎摸索。==一开始，几个页面都是 null，补下基础，区分 JS 中 null 和 undefine。null 就是没有内存，undefine 就是没有值，JS一声明变量就会有内存分配。  
	==抓住问题的本质，为什么慢，DOM的渲染。==必须知道，什么时候页面会加入 DOM 中，root ==AddChild== 的时候，就会加入 DOM 中。所以，先新建出来，然后是一个个去 AddChild。  
	==实现PageLayout 的 addChild方法。== GridLayout 已经实现了，先学习之。1、GridLayout 有 HasChild，AddChild，RemoveChild。2、children 就是一个数组。

