##1.    前言##

工作中，我们常常需要给javascript编写api文档。当然我们会借助一些工具，把文档注释抽取出来形成api文档。

我选择的是jsdoc这个工具。此前我根据这份[jsdoc文档模板](https://github.com/alivedise/jsdoc3-bootstrap)自定义了一些功能，并且我已经把我的修改提交给了作者。但是我在想了解这一切背后的jsdoc是一个怎么样的原理，以此作为课题，于是有了这一系列的文章。

##2.    背景知识##

###2.1  jsdoc注释语法###

如果你还不熟悉jsdoc的注释语法，你可以浏览下这份[在线文档](http://usejsdoc.org/)。

###2.2  NodeJS###

jsdoc这个工具允许你运行在[NodeJS](http://nodejs.org/)上，也可以直接使用Mozila Rhino来运行。不过我们主要的研究方向，还是在NodeJS上运行jsdoc。

###2.3  Mozila Rhino###

[Rhino](http://en.wikipedia.org/wiki/Rhino_(JavaScript_engine))是一个开放源代码的JavaScript引擎，由Java语言编写并且由Mozilla基金会维护。Mozila Rhino和[SpiderMonkey](http://en.wikipedia.org/wiki/SpiderMonkey_(JavaScript_engine))是不一样的引擎，SpiderMonkey也是由Mozilla开发，但是SpiderMonkey使用C语言编写并且使用在火狐浏览器上。

Rhino提供一下特性：

1. 支持所有[JavaScript 1.7](https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/1.7)的特性
1. 直接在Java代码里编写脚本
1. 包含一个[JavaScript Shell](https://developer.mozilla.org/en-US/docs/Rhino/Shell)直接执行JavaScript代码
1. 包含一个[JavaScript编译器](https://developer.mozilla.org/en-US/docs/Rhino/JavaScript_Compiler)，可以把脚本编译成Java字节码
1. 包含一个JavaScript调试器

**但jsdoc使用的是一个定制版的[Rhino](https://github.com/jsdoc3/rhino)。**

jsdoc的Rhino分支，主要添加了一下功能：

1. 支持JSDoc Comment格式的注释
1. 支持Node.js/CommonJS格式的包