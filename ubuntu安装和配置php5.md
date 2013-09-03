#ubuntu安装和配置php5,nginx#

##安装php5##

在linux下安装PHP简直太容易了，一行命令搞定一切：

	sudo apt-get -y install php5-common php5-cli php5-fpm

之后我们可以运行一下命令检查一下是否已经安装成功了：

	php -v

![php 5 install succ](./php5_install_succ.png)

##安装nginx##

如果你还米有安装nginx的话，请参考我的另外一篇博文[在ubuntu下安装nginx](http://my.oschina.net/knightuniverse/blog/157869)

##配置php5##

我们需要修改一下fpm的配置文件:
	
	sudo gedit /etc/php5/fpm/php.ini

找到**cgi.fix_pathinfo=1**这一行,然后把1改成0：

	cgi.fix_pathinfo=0

If this number is kept as 1, the php interpreter will do its best to process the file that is as near to the requested file as possible. This is a possible security risk. If this number is set to 0, conversely, the interpreter will only process the exact file path—a much safer alternative. Save and Exit. 

We need to make another small change in the php5-fpm configuration.Open up www.conf:

	 sudo gedit /etc/php5/fpm/pool.d/www.conf

Find the line, **listen = 127.0.0.1:9000**, and change the **127.0.0.1:9000** to **/var/run/php5-fpm.sock**.

	listen = /var/run/php5-fpm.sock

Save and Exit. Restart php-fpm:

	sudo service php5-fpm restart

>NOTE:我这边安装完php-fpm后，这个listen地址就是正确的了。

##配置nginx##

Open up the default virtual host file.

	sudo gedit /etc/nginx/sites-available/default

The configuration should include the changes below (the details of the changes are under the config information):

	server {
        listen   80;
     

        root /usr/share/nginx/www;
        index index.php index.html index.htm;

        server_name example.com;

        location / {
                try_files $uri $uri/ /index.html;
        }

        error_page 404 /404.html;

        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
              root /usr/share/nginx/www;
        }

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        location ~ \.php$ {
                #fastcgi_pass 127.0.0.1:9000;
                # With php5-fpm:
                fastcgi_pass unix:/var/run/php5-fpm.sock;
                fastcgi_index index.php;
                fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
                include fastcgi_params;
                
        }

	}

Here are the details of the changes:

+	Add index.php to the index line.
+	Change the server_name from local host to your domain name or IP address (replace the example.com in the configuration)
+	Change the correct lines in “location ~ \.php$ {“ section

Save and Exit

##测试php页面##

To set this up, first create a new file:
	
	sudo touch /usr/share/nginx/www/info.php
	sudo gedit /usr/share/nginx/www/info.php

Restart nginx

	sudo service nginx restart

You can see the nginx and php-fpm configuration details by visiting http://youripaddress/info.php

![phpinfo](./php5_phpinfo.png)

>PS:其实后来我又在centos上安装了nginx和php，过程其实大同小异。LINUX果然是一法通万法通。

	yum install php-common php-cli php-fpm
	wget http://nginx.org/keys/nginx_signing.key
	rpm --import nginx_signing.key
	yum update
	yum install nginx

>之后的php配置其实和上文是一样的，只不过在centos下不会写php5-fpm.sock，而是写php-fpm.sock，即前缀是php而不是php5。

>PS:这边其实还要注意一个问题，就是防火墙的问题。默认情况下，centos的防火墙并没有开放80端口，因此我们需要手工开放端口。

>开放80端口：

	iptables -I INPUT -p tcp --dport 80 -j ACCEPT

>保存防火墙配置：

	/etc/rc.d/init.d/iptables save

>这样重启计算机后,CentOS防火墙默认已经开放了80端口。不过我们也可以在不重启系统的情况下重新加载防火墙配置：

	/etc/init.d/iptables restart

>我们可以通过以下命令查看CentOS防火墙信息：

	/etc/init.d/iptables status

##参考文档##

1.	[How to Install Linux, nginx, MySQL, PHP (LEMP) stack on Ubuntu 12.04](https://www.digitalocean.com/community/articles/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-12-04)
2.	[PHP基础教程](http://www.w3school.com.cn/php/)
3.	[PHP 类与对象](http://www.5idev.com/p-php_class_object.shtml)
4.	[CentOS防火墙配置 80端](http://os.51cto.com/art/201003/191522.htm)