DiaSocial 问题
===
- 实现懒加载
	- 需求  
		WebView 初始化，太慢。目前解决思路有两种，使用 canvas 和懒加载。先试试懒加载。
	- 思维过程  
	
		==瞎摸索。==一开始，几个页面都是 null，补下基础，区分 JS 中 null 和 undefine。null 就是没有内存，undefine 就是没有值，JS一声明变量就会有内存分配。  
	
		==抓住问题的本质，为什么慢，DOM的渲染。==必须知道，什么时候页面会加入 DOM 中，root ==AddChild== 的时候，就会加入 DOM 中。所以，先新建出来，然后是一个个去 AddChild。 
 
		==学习 GridLayout 的 AddChild 方法。==    
		    
		1. GridLayout 有 HasChild，AddChild，RemoveChild。
		2. children 就是一个数组。
		3. Invalide，css 布局，visible 检测，遍历 children，一个个去设置 children 中每个元素的大小和位置。
		4. AddChild，先看元素是否在 children 数组中，如果在，就改变那个元素的位置，然后 invalide 一次。如果不在，先加入 children 数组，再加入 DOM 中，然后 invalidate 一次。
		5. AddChilde的重载，套几个数值，便可理解。
		6. RemoveChild，遍历 children 是否存在，如果存在，splice it，DOM 中 remove it，Invalite 一次。
		7. 由 Layout 去控制元素的显示，什么叫控制显示，调用元素的 AccessSize，AccessPosition，每一次 AccessSize，AccessPostion，都会调用元素的 Invalidate。    
		
		==学习 AbsoluteLayout 的 AddChild 方法。==    
		
		1. AbsoluteLayout 是 子元素去控制自己的显示。

		==实现 PageLayout 的 AddChild 方法。==  
		
		1. 没有思路，便分析，摸索，思考。
		2. PageLayout 目前已经有了一个构造方法，传入的参数为 Array，重载一个构造方法，传入的参数为 Object。不行，为什么不行？（不管三七二十一，先综合法，综合法适合于寻找思路。要想证明其不行，就假设其可行。）假设传入 Object，那就做吧。在大脑中想想其代码应该怎么写。
		3. 更简单方法，提供 AddChild 方法。
		4. Invalidate 应该做什么？Invalidate，遍历 children（pages） 数组，如果 visible，显示，不是，则不显示，每一个 child（page）的大小和 容器一样。

		==实现主页四个页面的懒加载==
		
		1. ==本质是什么？==当点击每个 nav_button 的时候，生成 page，将 page AddChild 进 PageLayout 中。
		2. PageLayout.AccessActivePage，设置哪一个 page 是 Active 的，然后 Invalidate 一下。
		3. btn.Register，在页面 initialize 上 register 事件，在实际的 click 时候，会 emit 事件。
		4. Navigator 里有个 InitialzeUI，是在什么触发的？在异步转同步工作流中。
		5. ==就是不知道动手，我该怎么办？脑中想象代码。==一个pages 数组，这个数组，一开始只有一个 page，也就是第一个页面。将这个 pages 数组传给 PageLayout 的构造函数。当点击 nav_button 的时候，就把那个 page AddChild 进 PageLayout 里。再次点击，page 会再次被 AddChild 进 PageLayout 中，这个时候，PageLayout 中已经做好这个处理了，AddChild 时候，先检查是否在，在的话，直接 return。点击 nav_button 之后，page AddChild，ActivePage。
	
		==总结==　pages，只有一个元素，生成 PageLayout，每次 nav_button 的点击，AddChild，ActivePage。
		==但是==　还是没有效果，需 7s 才可以加载。我猜是不是 JS 的原因，需要测试一下。
		
		
- 点击事件延迟
	- ==出现场景==　WebView 点击事件延迟。
	- ==为什么==　查阅资料说是 300ms 延迟事件，为了区分单击和双击，但是我这不止 300ms 啊。
	- ==怎么办==　

		1. console.log 一点点测时间，到底哪儿出问题了。1.测试 Android Studio 是否会显示 console.log 的信息；2.JavaScript打印时间。

		    
				

