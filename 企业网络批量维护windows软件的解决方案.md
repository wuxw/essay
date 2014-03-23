##  前言

本人不是专业的运维人员，只是对运维挺感兴趣的。业余时间忽然在想，假如公司的IT部门，要在整个公司范围内，批量部署和更新windows的软件，有哪些可选方案。

于是有了这篇博客，不过我想应该有很多问题，欢迎斧正。

##  可选方案

1.  [WSUS](http://wenku.baidu.com/view/be1ff53bdd36a32d737581bf.html)
2.  [System Center Configuration Manager](http://searchwindowsserver.techtarget.com/definition/Microsoft-System-Center-Configuration-Manager-2012)

**WSUS**

Windows Server Update Services(简称WSUS)，是微软公司提供的一种免费软件，它提供了Windows部分操作系统的关键更新的分发。网络中心基于此技术在岛内构建了一个WSUS服务器，向全岛的网络用户提供免费的WSUS服务，使用此服务，可以快速进行部分Windows操作系统的关键补丁的更新，减轻在病毒发作时从美国微软更新的时间，同时通过运行如下所附的设置程序将会将您的计算机的更新完全调节好，从而免除您担心更新问题的烦恼。  

WSUS目前提供了对微软15个新产品和8个新分类的更新，产品其中涵盖了Windows　2000家族、Windows　XP家族、Windows　2003家族、Office 2000/xp／2003家族、SQL　SERVER等，提供更新的8个分类为：Feature Pack、Service Pack、安全更新程序、更新程序、更新程序集、工具、关键更新程序、驱动程序，当适用于您的计算机的重要更新发布时，它会及时提醒您下载和安装。使用自动更新可以在第一时间更新您的操作系统以及其它微软产品，修复系统及程序的漏洞，保护您的计算机安全。使用此更新同微软的在线升级并无冲突，此更新系统可同步微软网站更新的一半以上都是一些关键更新，为使补丁完全您仍然可以随时访问

**System Center Configuration Manager**

SCCM是微软旗下的一个管理软件，用于管理企业内部设备，软件的部署以及安全维护。关于SCCM，我们有以下的Blog：

1.   [安装前准备](http://rdsrv.blog.51cto.com/2996778/1134717)
1.   [安装部署SCOM](http://rdsrv.blog.51cto.com/2996778/1134727)
1.   [导入管理包](http://rdsrv.blog.51cto.com/2996778/1147618)
2.   [邮件通知(上)](http://rdsrv.blog.51cto.com/2996778/1149466)
3.   [邮件通知(下)](http://rdsrv.blog.51cto.com/2996778/1150259)
4.   [即时消息通知(上)](http://rdsrv.blog.51cto.com/2996778/1151582)
5.   [即时消息通知(下)](http://rdsrv.blog.51cto.com/2996778/1152170)
6.   [单台服务器拓扑监控](http://rdsrv.blog.51cto.com/2996778/1152977)
7.   [创建组集合](http://rdsrv.blog.51cto.com/2996778/1154663)
8.   [单台服务器性能图监控](http://rdsrv.blog.51cto.com/2996778/1154665)