##初衰##

之前一直在Windows上进行开发，用着用着其实也还好。久了，总感觉windows不够酷，何况做前端开发工作，并不一定要使用Windows平台。另外，我这个人又挺喜欢折腾的，加之我认为LINUX才是未来大势所趋：很多互联网系统后端架构在LINUX上，各种手持设备，你身边的电视机定盒，遥控器，或者车载系统，包括NASA上部署的操作系统，都是LINUX。掌握LINUX很重要。

##Distro##

[Linux mint](http://www.linuxmint.com/)

linux mint是ubuntu的衍生版，单从界面操作角度来看，Linux Mint更偏向Windows界面，对于广大Windows用户而言，上手并不困难。

我选择Mint而不是Ubuntu一个主要原因就是：我非常不喜欢Unity。我曾经用过一段时间的Ubuntu10.0，但我完全不习惯Unity界面。那时候Unity界面才刚出，不是很稳定，兼容性也做的不够。此外，使用Ubuntu，有些音频视频的解码器还要自己安装，光是一个flash的安装就能搞死你了。Mint这一切都帮你搞定了，真正做到了开箱即用。

##工作日记##


1.  [Almanah Diary](https://wiki.gnome.org/Almanah_Diary)   

    ![Almanah Diary](http://tecnocode.co.uk/wp-content/uploads/2008/11/screenshot-almanah-diary-1.png)

在Windows下工作的时候我经常使用[DailyPIM](http://www.dailypim.com/)这个软件来编写工作日志。 DailyPIM是一款优秀的个人信息管理软件,具有的功能有日记本、资料管理、文件管理、日程管理等很多优秀的功能，而且能够自动按照日期归档日志，这一点是非常方便的。

切换到LINUX下暂时没有找打到较好的日志软件。Almanah Diary相对简陋了很多，不过纯粹用来记流水帐的工作日志，其实也够用了。

##代码管理##

1.  svn

现在软件公司都有采用源代码管理系统，其中SVN用的会比较多。Windows下的SVN客户端[TortoiseSVN](http://tortoisesvn.net/downloads.html)以其友好的GUI设计，易用性征服了所有的程序员，在LINUX下就没有这么好康的事情了，相对苦逼了许多。不过我们还是有这么两个不错的GUI客户端：   

+  [RapidSvn](http://community.linuxmint.com/software/view/rapidsvn)   
    
![RapidSvn](http://rapidsvn.tigris.org/screenshots/linux-1024x768-1.png)    
    
+  [eSvn](http://zoneit.free.fr/esvn/index.php)    
    
![eSvn](http://zoneit.free.fr/esvn/img/612-ss1_o.png)
    
+  [RabbitVCS](http://www.rabbitvcs.org/)  
    
![RabbitVCS](http://www.rabbitvcs.org/images/screenshots/git-log.png)
    
目前我自己使用的是RapidSvn。就上面的截图来看，似乎是RabbitVCSn的UI设计会是最好的。我想我应该尝试使用下，RapidSvn给我的感觉还是有点粗糙的，虽然它确实能搞定事情。关于在LINUX下如何安装RabbitVCS，[可以参考这篇博文](http://xfeng.me/linux-svn-tool-rabbitvcs/)，或者直接在[官网下载安装](http://wiki.rabbitvcs.org/wiki/download)。在LINUX下，要是代码有冲突了，处理起来就完全没有那么方便了。目前我并没有遇到代码冲突的情况（刚接触LINUX同时还是自己一个人做项目...），我想慢慢地我也得去看下怎么处理冲突了，如果各位同学有好的资料，不妨给我留言 :)

2.  Git

实际上我私人也用Git的。Linux下一般我都是直接使用命令行的。入门的话，我感觉这个[Git Reference](http://gitref.org/)站点不错。

最近试用[meld](http://meldmerge.org/)，这是GIT的一个mergetool，能同时支持多个代码管理系统以及多个系统平台。

![meld](http://meldmerge.org/images/meld-filediff-full.png)

>NOTE:另外一个比较常用的是KDiff3，这个软件看起来也是相当不错的，不过我不经常使用就是了。

GIT代码库的图形化GUI，个人推荐[Cola Git Gui](http://git-cola.github.io/)。

![Cola Git Gui](http://git-cola.github.io/images/dag.png)

##编辑器##

1.  [Sublime text 2](http://www.sublimetext.com/)

![Sublime text 2](http://www.designerstalk.com/forums/attachments/software/11468d1329991697-sublime-text-2-sublime.jpg)

Sublime text 2是一个性感无比的代码编辑器！强烈推荐！[Mint下安装Sublime text editor](http://community.linuxmint.com/tutorial/view/907)也非常容易。安装成功之后，[额外再安装几个插件](http://www.iplaysoft.com/sublimetext.html)，可以瞬间让你的编码效率提高很多。

2.  [Retext](http://sourceforge.net/projects/retext/),

![Retext](http://blog.sudobits.com/wp-content/uploads/2012/10/live-preview-ReText.jpg)

Retext是一个[Markdown](http://en.wikipedia.org/wiki/Markdown)编辑器。

我偶尔会写写博客啊什么的。但是我非常不喜欢直接使用各个网站提供的所见即所得HTML编辑器，这些编辑器给我的感觉就是非常没有效率！在网上查看是否有更高效的方案的时候，我发现了[Markdown](http://en.wikipedia.org/wiki/Markdown)这个语言。

Markdown 的目标是实现「易读易写」，实际上它确实做到了：它是一个适用于网络的书写语言。这边有一篇[Markdown 语法说明 (简体中文版)](http://wowubuntu.com/markdown/)可以快速入门，只需要半个小时就可以完全入门。使用Markdown编写博文是非常惬意，一目了然的。

这篇博文也是使用Retext编写的 :)

##界面原型图绘制工具##

1.  [Pencil](http://pencil.evolus.vn/)

Pencil 是一款开源的原型图绘制工具，手绘风格的，就像自己在纸上画的那样。你还可以用它来绘制各种架构图和流程图。撰写这篇博文的时候，我才刚开始使用这款软件，不过第一感觉这个软件非常不错！

![Pencil](http://static.oschina.net/uploads/img/201105/30220353_D76f.jpg)

##后续##

我想，这篇博文应该是会持续更新的。在LINUX下工作，我还有很多东西要学，要记录，好记性不如烂笔头。
