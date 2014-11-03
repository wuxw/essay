##问题描述

今天Q群里，有个朋友问了我这么一个问题：“js可以判断一段文字，是否有回车吗？如果有回车的话，可以把回车过滤掉吗？”

这个问题本身并不难，用正则表达式就能很轻易的过滤掉。花了不到5分钟的时间，我快速出了一个DEMO，代码如下：

    <!DOCTYPE html>
    <html>
    <head>
    
    </head>
    <body>
    
	    <textarea id="t" rows="4" cols="50">
	    At w3schools.com you will learn how to make a website.
	    
	    
	    
	    We offer free tutorials in all web development technologies. 
	    </textarea>
	    
	    <script>
	    
		    var dom = document.getElementById('t');
		    var val = dom.value;
		    var re = /\r|\n/g;
		    var rip = val.replace(re,"");
		    
		    console.log(rip);
	    
	    </script>
    
    </body>
    </html>

有另外一个同学就问了：“回车是`var re = /\r|\n/g;`吗？回车不是单独的`\n`吗？”

我印象中，不同的系统之间，回车换行处理方式好像是不一致的，但是细节上我的确是没有搞清楚。挖掘机还是要找蓝翔的，那`\n\r`还是`\r`这个问题只能找谷歌了。

##回车换行的历史

![Underwoodfive.jpg](./Underwoodfive.jpg)

Long long ago，当时的计算机使用一种叫做[`Teletype Model 33 ASR`](http://en.wikipedia.org/wiki/Teletype_Model_33)作为终端。当时，这种`Teletype`有一个约定：使用`CR + LF`来表示换行。

`LR(a.k.a Line Feed)`意思就是要打字机切换到新的一行上接着打印，而`CR(a.k.a Carriage Return)`指示打字机将打印设备定位到一行的开头。

**为什么需要两个控制字符来表示换行？**

早期的打字设备有一个关于`Carriage Return`比较严重的问题，但这个问题我不大清楚是怎么一回事，维基百科是这么描述的：

>Early teletype machines had a problem when a printing character followed the carriage return. It just printed it as a smudge, on-the-fly in the middle of the page, while it was moving the carriage back to the first position. "The solution was to make the newline two characters: CR to move the carriage to column one, and LF to move the paper up."

是的，为了解决上面的问题，所以使用了`LF`把纸往上移动一行，然后在用`CR`把打印设备定位到第一列。

**这是硬件方面的问题，计算机为什么也用 `CR + LF` 表示换行？**

在那个时候，设备驱动的概念还没有出现。换句话说，就是还没有一种技术可以隐藏这些底层硬件设备之间的区别，应用程序必须负责处理这些细节上的问题。当时应用程序的做法是直接采纳了`Teletype`的`CR + LF`换行这一约定。

这里还有一些其他的历史原因，早期的DEC微型计算机直接使用`CR + LF`换行这一约定。后来MS-DOC出于程序兼容方面的考虑，故而还是采纳了`CR + LF`换行这一约定，这一约定在Windows操作系统中也被保留了下来。

另外，当时的多任务操作系统只使用`LF`作为换行符。当时的多任务操作系统已经开始使用设备驱动来屏蔽底层硬件的区别了，所以上层应用程序编写起来就相对方便多了。大名鼎鼎的`Unix`操作系统保留了这一处理方式，而`Unix`后面的操作系统则效仿`Unix`的做法。

>NOTE: DEC(Digital Equipment Corporation)，既美国数字设备公司。1998年1月DEC公司被康柏以96亿美元的价格收购，2001年惠普康柏宣布合并。

**其他答案**

当我用中文搜索的时候，比如[这篇博文](http://www.cnblogs.com/me115/archive/2011/04/27/2030762.html)，作者的解答是这样的：

>在计算机还没有出现之前，有一种叫做电传打字机（Teletype Model 33，Linux/Unix下的tty概念也来自于此）的玩意，每秒钟可以打10个字符。但是它有一个问题，就是打完一行换行的时候，要用去0.2秒，正好可以打两个字符。要是在这0.2秒里面，又有新的字符传过来，那么这个字符将丢失。
>
>于是，研制人员想了个办法解决这个问题，就是在每行后面加两个表示结束的字符。一个叫做“回车”，告诉打字机把打印头定位在左边界；另一个叫做“换行”，告诉打字机把纸向下移一行。这就是“换行”和“回车”的来历，从它们的英语名字上也可以看出一二。
>
>后来，计算机发明了，这两个概念也就被般到了计算机上。那时，存储器很贵，一些科学家认为在每行结尾加两个字符太浪费了，加一个就可以。于是，就出现了分歧。

然后很多的中文博客用的都是这么一个答案。我不知道`电传打字机`的研发过程是怎样的，对比维基百科的解释，我觉得这个答案**严重，极其不靠谱**。

##参考

1.	[Newline](http://en.wikipedia.org/wiki/Newline)
2.	[Multics](http://en.wikipedia.org/wiki/Multics)
3.	[Typewriter](http://en.wikipedia.org/wiki/Typewriter)
4.	[Teletype Model 33](http://en.wikipedia.org/wiki/Teletype_Model_33)