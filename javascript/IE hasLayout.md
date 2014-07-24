##1.	简介

**原文出自：**[IE hasLayout](http://haslayout.net/haslayout)

我平时写CSS相对较少，但是一些CSS的陷阱还是有所听说。今天在查阅一些CSS资料的时候，无意间遇到了这个haslayout的问题，于是就顺手整理了下。

**注意：**hasLayout这个属性，在IE8标准模式以及IE8以上版本的IE浏览器中，已经不生效。但在IE7兼容模式下，这个hasLayout属性依然发挥作用。

##2.	为什么会有hasLayout？

旧版的IE浏览器中，比如IE5，IE6等，使用一个相当古老的HTML排版引擎（原文指出这个排版引擎是[Mosaic](http://en.wikipedia.org/wiki/Mosaic_web_browser)，我上维基百科看了下，我想应该是真的。如果HTML的历史稍微有一些印象的话，应该会知道，在HTML成为标准之前，Mosaic是非常牛叉的一款浏览器）。

旧时代的WEB基本都是使用table进行布局的，这个时候一般是不会有内容overflow的问题产生。之后，微软在其IE浏览器中使用的[Trident](http://en.wikipedia.org/wiki/Trident_(layout_engine))排版引擎引入了对CSS的支持。但是CSS改变了游戏规则，因为CSS允许HTML元素的内容超过元素的宽高，这种情况有可能发生在了float或者元素内容超出容器定义的宽高，也就是overflow。

##3.	hasLayout从何而来？

微软的工程师使用了一种比较奇葩的方式解决上面提到的问题——`hasLayout`属性诞生了。所有的HTML元素都有一个`hasLayout`属性，并且可以设置成`true`或者`false`。

如果`hasLayout`属性为`true`，那么这个元素就要花更多代价去渲染自己，它必须负责为自己和可能的子孙元素进行尺寸计算和定位。

如果`hasLayout`属性为`false`，那么这个元素就要依靠某个祖先元素来渲染它。

>NOTE: 虽然是这么说的，但是有机会我还是应该去找几个DEMO看看，不然还是对这个问题不是很清楚。

`hasLayout`不是标准的CSS属性，这是微软的一个拓展属性，并且是只读属性——你无法通过CSS样式表，例如`hasLayout: true;`，或者是Javascript，`el.currentStyle.hasLayout = true;`去设置。一个元素是否`hasLayout`，关键就是`hasLayout`属性值是否是`true`。

##4.	默认情况下，哪些HTML元素有hasLayout属性？

-	```<html>, <body>```
-	```<table>, <tr>, <th>, <td>```
-   ```<iframe>, <embed> (non-standard element), <object>, <applet>```
-   ```<img>```
-   ```<hr>```
-   ```<input>, <button>, <select>, <textarea>, <fieldset>, <legend>```
-   ```<marquee> (最好别用这个元素，非标准元素)```

这些元素可能不够全面，可能还有一些其他元素没有在上面的列表中，那么，如何去测试元素的`hasLayout`属性值？

假设我们有这么一个`div#menu`元素：

    <div id="menu">
    ...
    </div>

我们可以通过以下代码去获取`hasLayout属性`的值：

    var $menu = document.getElementById( 'menu' );
    console.log( $menu.currentStyle.hasLayout );

##5.	通过CSS属性设置`hasLayout`的值

要让元素的`hasLayout`属性值为`true`，相对设置成`false`而言，是件容易的事情。以下的CSS属性/值，可以设置元素的`hasLayout`属性值为`true`：

- **position:** absolute
- **float:** left | right
- **display:** inline-block
- **width:** 非auto的任意值
- **height:** 非auto的任意值
- **zoom:** 非normal的任意值
- **writing-mode:** tb-rl

在**IE7**，还有以下这些CSS属性/值生效：

- **overflow:** hidden | scroll | auto
- **overflow-x:** hidden | scroll | auto
- **overflow-y:** hidden | scroll | auto
- **min-width:** 非auto的任意值
- **max-width:** 非auto的任意值
- **min-height:** 非auto的任意值
- **max-height:** 非auto的任意值



