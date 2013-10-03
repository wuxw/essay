##问题描述##

使用[loadmask.js](https://code.google.com/p/jquery-loadmask/)做loading样式的时候，loadmask库创建了一个div.loadmask的遮罩层。这个遮罩层在Chrome，Opera，Safari，Firefox下**正确遮罩住z-index比它小的元素**，但是在IE下失败了。

也就是说，**在IE系列的浏览器下，z-index没有生效**。

在**zIndex错误页面**，正常情况下，位于**遮罩层后面**的元素（比如“新增”按钮）应该是**无法点击**的，但是因为IE浏览器z-index的BUG，导致现在我们依然可以点击新增按钮：

![zIndex错误页面](./zIndex_error_page.png)

**div.loadmask**的样式如下所示：

![div.loadmask](./zIndex_div_loadmask.png)

loadmask.js动态添加在**body**元素上的样式如下所示：

![body](./zIndex_body.png)

##解决方案##

在上图所示的loadmask类中，加入以下CSS样式，即可搞定问题：
	
	background-color:white;
	opacity: 0;
	filter: alpha(opacity=0);/*for IE5-7*/ 
	-ms-filter:"progid:DXImageTransform.Microsoft.Alpha(Opacity=0)";/*for IE8*/

##问题产生的原因##

This is how z-index should work according to the [spec](http://www.w3.org/TR/CSS2/visuren.html#z-index):

+	you can give a z-index value to any element; 

+	if you don't, it defaults to auto
positioned elements (that is, elements with a position attribute different from the default static) with a z-index different from auto create a new stacking context. Stacking contexts are the "units" of overlapping; one stacking context is either completely above the another (that is, every element of the first is above any element of the second) or completely below it.

+	inside the same stacking context, the stack level of the elements is compared. Elements with an explicit z-index value have that value as a stack level, other elements inherit from their parents. The element with the higher stack level is displayed on top. When two elements have the same stack level, generally the one which is later in the DOM tree is painted on top. (More complicated rules apply if they have a different position attribute.)
In other words, when two elements have z-index set, in order to decide which will show on top, you need to check if they have any positioned parents which also have z-index set. If they don't, or the parents are common, the one with the higher z-index wins. If they do, you need to compare the parents, and the z-index of the children is irrelevant.

So the z-index decides how the element is placed compared to other children of its "stacking parent" (the closest ancestor with a z-index set and a position of relative, absolute or fixed), but it doesn't matter when comparing to other elements; it is the stacking parent's z-index (or possibly the z-index of the stacking parent's stacking parent, et cetera) which counts. In a typical document where you use z-index only on a few elements like dropdown menus and popups, none of which contains the other, the stacking parent of all the elements which have a z-index is the whole document, and you can usually get away with thinking of the z-index as a global, document-level ordering.

The fundamental difference with IE6/7 is that positioned elements start new stacking contexts, whether they have z-index set or not. Since the elements which you would instinctively assign z-index values to are typically absolutely positioned and have a relatively positioned parent or close ancestor, this will mean that your z-index-ed elements won't be compared at all, instead their positioned ancestors will - and since those have no z-index set, document order will prevail.

As a workaround, you need to find out which ancestors are actually compared, and assign some z-index to them to restore the order you want (which will usually be reverse document order). Usually this is done by javascript - for a dropdown menu, you can walk through the menu containers or parent menu items, and assign them a z-index of 1000, 999, 998 and so on. Another method: when a popup or dropdown menu becomes visible, find all its relatively positioned ancestors, and give them an on-top class which has a very high z-index; when it becomes invisible again, remove the classes.

##参考文档##

1.	[Overlapping And ZIndex](http://css-discuss.incutio.com/wiki/Overlapping_And_ZIndex)
2.	[Squish the Internet Explorer Z-Index Bug](http://www.brenelz.com/blog/squish-the-internet-explorer-z-index-bug/)
3.	[Fiddler – Put a breakpoint in your network traffic…](http://blog.alner.net/archive/2008/10/06/fiddler-ndash-put-a-breakpoint-in-your-network-traffichellip.aspx)
4.	[IE 6 & IE 7 Z-Index Problem](http://stackoverflow.com/questions/672228/ie-6-ie-7-z-index-problem)