首先安装EPEL：

	wget http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
	rpm -ivh epel-release-6.8.noarch.rpm

接着安装GIT：

	yum install git

完成GIT安装之后，首先要添加SSH KEY了。一开始，我遇到这么一个问题：

	 "Could not open a connection to your authentication agent"

这个问题其实也很好搞定，设置（虽然我也搞不清楚为什么要这么设置）

	ssh-agent /bin/bash

接着添加SSH KEY，但是我又遇到这样的问题：

	ssh “permisssions are too open” error

这个问题其实是因为你的SSH KEY文件权限太高了，设置成只读权限，问题就搞定了：

	chmod 400 ~/.ssh/id_rsa

完成SSH KEY的添加：

	ssh-add ~/.ssh/id_rsa

然后你就可以开始Clone Git Repo了！

##参考文档##

1.	[Error "Could not open a connection to your authentication agent"](http://blackboard.myhomepc.in/2010/04/error-could-not-open-connection-to-your.html)
2.	[Install Git on CentOS 6](http://blog.zwiegnet.com/linux-server/install-git-on-centos-6/)
3.	[ssh “permisssions are too open” error](http://stackoverflow.com/questions/9270734/ssh-permisssions-are-too-open-error)