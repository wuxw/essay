##[前言]##

这几天上网无意间看到一个新名词：Javascript Harmony。联想到以前的ES 5等，瞬间让我觉得我对javascript的相关版本的概念一直都很模糊。因此决定好好研究下相关的信息。

##[正文]##

### 1. Javascript的定义###

一个完整的 JavaScript 实现是由以下 3 个不同部分组成的:

	*	核心（ECMAScript）
	*	文档对象模型（DOM）
	*	浏览器对象模型（BOM）

#### 1.1 ECMAScript ####

ECMAScript是一种由[Ecma国际](https://zh.wikipedia.org/wiki/Ecma%E5%9B%BD%E9%99%85)（[前身为欧洲计算机制造商协会](https://zh.wikipedia.org/wiki/%E6%AC%A7%E6%B4%B2%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%88%B6%E9%80%A0%E5%95%86%E5%8D%8F%E4%BC%9A)）通过ECMA-262标准化的脚本程序设计语言。

ECMAScript 仅仅是一个描述，定义了脚本语言的所有属性、方法和对象，并不与任何具体浏览器相绑定。实际上，它也没有提到用于任何用户输入输出的方法（这点与 C 这类语言不同，它需要依赖外部的库来完成这类任务）。Web 浏览器对于 ECMAScript 来说是一个宿主环境，但它并不是唯一的宿主环境。事实上，还有不计其数的其他各种环境（例如 Nombas 的 ScriptEase，以及 Macromedia 同时用在 Flash 和 Director MX 中的 ActionScript）可以容纳 ECMAScript 实现。

ECMAScript 描述了以下内容：

*	语法
*	类型
*	语句
*	关键字
*	保留字
*	运算符
*	对象

JavaScript只是ECMAScript的实现和拓展。

#### 1.2 文档对象模型（DOM） ####

DOM（文档对象模型）是 HTML 和 XML 的应用程序接口（API）。DOM 将把整个页面规划成由节点层级构成的文档。DOM定义了表示和修改文档所需的对象、这些对象的行为和属性以及这些对象之间的关系。可以把DOM认为是页面上数据和结构的一个树形表示，不过页面当然可能并不是以这种树的方式具体实现。

通过 DOM API，你可以重构整个HTML文档。你可以添加、移除、改变或重排页面上的项目。

##### 1.2.1 DOM的不同的部分 #####

*	Core DOM<br /><br />定义了一套标准的针对任何结构化文档的对象<br /><br />
*	XML DOM<br /><br />定义了一套标准的针对 XML 文档的对象<br /><br />
*	HTML DOM<br /><br />定义了一套标准的针对 HTML 文档的对象。

##### 1.2.2 DOM的各个level #####

*	Level 1
*	Level 2
*	Level 3

其他DOM
除了 DOM Core 和 DOM HTML 外，还有其他几种语言发布了自己的 DOM 标准。这些语言都是基于 XML 的，每种 DOM 都给对应语言添加了特有的方法和接口：


#### 1.3 浏览器对象模型（BOM）####

IE 3.0 和 Netscape Navigator 3.0 提供了一种特性 - BOM（浏览器对象模型），可以对浏览器窗口进行访问和操作。使用 BOM，开发者可以移动窗口、改变状态栏中的文本以及执行其他与页面内容不直接相关的动作。使 BOM 独树一帜且又常常令人怀疑的地方在于，它只是 JavaScript 的一个部分，没有任何相关的标准。

BOM 主要处理浏览器窗口和框架，不过通常浏览器特定的 JavaScript 扩展都被看做 BOM 的一部分。这些扩展包括：

*	弹出新的浏览器窗口
*	移动、关闭浏览器窗口以及调整窗口大小
*	提供 Web 浏览器详细信息的定位对象
*	提供用户屏幕分辨率详细信息的屏幕对象
*	对 cookie 的支持
*	IE 扩展了 BOM，加入了 ActiveXObject 类，可以通过 JavaScript 实例化 ActiveX 对象

### 2. Javascript的历史 ###

1.	1992年 C--诞生

	一家称作Nombas的公司开始开发这种语言。这个脚本语言捆绑在一个叫做CEnvi的共享软件产品中，当Netscape Navigator崭露头角时，Nombas开发了一个可以嵌入网页中的CEnvi的版本。现在一般将这些早期的试验称为EspressoPage（浓咖啡般的页面），它们代表了第一个在万维网上使用的客户端脚本语言。不过[周爱民](http://blog.csdn.net/aimingoo/)[考证](http://blog.csdn.net/aimingoo/article/details/1932315)之后，认为第一个在万维网上使用的客户端脚本语言应该是Javascript而不是Espresso Page。您也可以参考[博客园知识](http://kb.cnblogs.com/page/140723/)库进一步深入。

2.	1995年 Netscape Navigator 2.0发布，带来了**Javascript 1.0**，同年，IE 1.0以及2.0发布。

	JavaScript一开始的命名是LiveScript，用于解决简单的处理问题，比如验证客户端表单的正确性。当时大部分因特网用户还仅仅通过28.8 kbit/s的调制解调器连接到网络，仅仅为了简单的表单有效性验证，就要与服务器进行多次地往返交互，这种体验是非常糟糕的。
	就在 Netscape Navigator 2.0 即将正式发布前，Netscape 将其更名为 JavaScript，目的是为了利用 Java 这个因特网时髦词汇。

3.	1996年 Netscape Navigator 3.0发布，带来了**Javascript 1.1**，此版本有分为「Standard Edition」和「Gold Edition」两个版本。IE 3.0发布。

4.	1997年 **JavaScript 1.1**作为一个草案提交给[欧洲计算机制造商协会](https://zh.wikipedia.org/wiki/Ecma%E5%9B%BD%E9%99%85)（ECMA），与此同时，Netscape Navigator 4.0~4.05发布，带来了**JavaScript 1.2**版。IE 4.0发布。

	由来自 Netscape、Sun、微软、Borland 和其他一些对脚本编程感兴趣的公司的程序员组成的[TC39](http://www.ecma-international.org/memento/TC39.htm)锤炼出了 ECMA-262，该标准定义了名为 ECMAScript 的全新脚本语言。

5.	1998年 Navigator 4.06~4.7发布，JavaScript升级到**JavaScript 1.3**版。

5.	1999年 **ECMAScript 3th**发布，带来了强大的正则表达式，更好的文字处理，新的控制指令，异常处理，错误定义更加明确，输出得格式化等。IE 5.0发布。

6.	2000年 Netscape 6.0发布。IE 5.5发布。带来了JavaScript 1.5版本。

7.	2001年 IE 6.0发布。

8.	2006年 IE 7.0发布。

9.	2009年 IE 8.0发布。

10.	2011年 IE 9.0发布。

<p>
<table>
	<caption>JScript与IE对ECMA的支持</caption>
	<tr><td>语言版本</td><td>浏览器版本</td><td>遵循标准</td></tr>
	<tr><td>JScript1.0</td><td>Internet Explorer 3.0</td><td>ECMA-262 版本 1</td></tr>
	<tr><td>JScript3.0</td><td>Internet Explorer 4.0</td><td>ECMA-262 版本 1</td></tr>
	<tr><td>JScript5.0</td><td>Internet Explorer 5.0</td><td>ECMA-262 版本 1</td></tr>
	<tr><td>JScript5.5</td><td>Internet Explorer 5.5</td><td>ECMA-262 版本 3</td></tr>
	<tr><td>JScript5.6</td><td>Internet Explorer 6.0</td><td>ECMA-262 版本 3</td></tr>
</table>
<br/>
<table>
	<caption>JavaScript与NS对ECMA的支持</caption>
	<tr><td>语言版本</td><td>浏览器版本</td><td>遵循标准</td></tr>
	<tr><td>JavaScript1.0</td><td>NetScape 2</td><td>ECMA-262 版本 1</td></tr>
	<tr><td>JavaScript1.2</td><td>NetScape 4.0~4.05</td><td>ECMA-262 版本 1</td></tr>
	<tr><td>JavaScript1.3</td><td>NetScape 4.06~4.7</td><td>ECMA-262 版本 1</td></tr>
	<tr><td>JavaScript1.4</td><td>无（仅服务器端）</td><td>ECMA-262 版本 1</td></tr>
	<tr><td>JavaScript1.5</td><td>NetScape 6.x与7.x</td><td>ECMA-262 版本 3</td></tr>
</table>
</p>

##[名词解释]##

2.Harmony

It's ES6.
A new code-name for a language which is to come after ES3.1. It will feature many of the things ES4 was trying to accomplish, but may attempt them from different directions and will
focus much more on incremental, step-wise evolution of the language.

3.ECMAScript 3.1

Aka: ES3.1. A set of small additions to ES3.

4.ECMAScript 4

Aka: ES4, “JavaScript 2?.
A new language which was to be mostly backwards compatible but add optional (gradual) typing and class-based inheritance. Based loosely on Adobe’s ActionScript 3. This is the language effort which died as a result of Harmony.

[参考文档]

1.	[JavaScript 实现](http://www.w3school.com.cn/js/pro_js_implement.asp)
2.	[各个版本的javascript新特性](https://developer.mozilla.org/en-US/docs/JavaScript/New_in_JavaScript)
3.	[the future of javascript](http://blog.chromium.org/2012/02/future-of-javascript-take-peek-today.html)
4.	[ECMAScript](https://zh.wikipedia.org/wiki/ECMAScript)
5.	[ECMAScript Harmony](https://mail.mozilla.org/pipermail/es-discuss/2008-August/006837.html)
6.	[John Resig-ECMAScript Harmony](http://ejohn.org/blog/ecmascript-harmony/)
7.	[Late binding](http://en.wikipedia.org/wiki/Late_binding)
8.	[ECMAScript 6 support in Mozilla](https://developer.mozilla.org/en-US/docs/JavaScript/ECMAScript_6_support_in_Mozilla)
9.	[[译]ECMAScript.next:TC39 2012年9月会议总结](http://www.cnblogs.com/ziyunfei/archive/2012/10/23/2734508.html)
10.	[New JavaScript Engine Module Owner](http://brendaneich.com/2011/06/new-javascript-engine-module-owner/)
11.	[还原JavaScript的真实历史](http://blog.csdn.net/aimingoo/article/details/1932315)
12.	[详图实证：再谈JavaScript的语源问题](http://kb.cnblogs.com/page/140723/)
13.	[ECMAScript](http://book.51cto.com/art/201006/207147.htm)