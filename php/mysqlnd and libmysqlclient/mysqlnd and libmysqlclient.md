## 1. PHP拓展 ##

### 1.1 PHP核心 ###

PHP的核心是由两个独立的部分组成的。

**在最底层是Zend Engine (ZE)**。ZE 负责把人类可以理解的脚本解析成机器可以理解的符号（token），然后在一个进程空间内执行这些符号。ZE还负责内存管理，变量作用域，以及函数调用的调度。

**另一部分是PHP**。PHP负责与SAPI层（Server Application Programming Interface，经常被用来与Apache, IIS, CLI, CGI等host环境进行关联）的交互以及绑定。它也为safe_mode和open_basedir检查提供了一个统一的控制层，就像streams层把文件和网络I/O与用户空间函数（例如fopen()，fread()和fwrite()）关联起来一样。

### 1.2 拓展形式 ###

+	PEAR。PEAR是PHP扩展与应用库（the PHP Extension and Application Repository）的缩写。它是一个PHP扩展及应用的一个代码仓库，简单地说，PEAR就是PHP的CPAN（Perl第三方代码库）。


+	PECL。PECL（PHP Extension Community Library），PHP的扩展库，它提供了一系列已知的扩展库，由C++等其他语言编写而成，以.so形式出现，.so 为共享库,是shared object,用于动态连接的,和dll差不多，为比PEAR更快，但是与PEAR不同的是，PECL需要在服务器上配置并被注册到主机中。

**最直接的表述：Pear是PHP的上层扩展，Pecl是PHP的底层扩展。**

## 2. MYSQL拓展 ##

### 2.1 如何访问MYSQL数据库 ###

可以使用的PHP拓展有这么几个：

1. mysql
1. mysqli
1. pdo

其中因为mysql是面向过程的，而且无法使用新版本MySQL带来的一些高级特性，现在已经不推荐使用。推荐使用mysqli以及pdo拓展。

但是这三种数据库访问方式，在PHP拓展的角度上看，还是比较上层的拓展，依赖**更底层的库**去连接和访问数据库。

**底层的库**，我们目前有这么两个：

1. libmysqlclient
1. mysqlnd

但是[决定使用这两个库中的那一个](http://www.php.net/manual/en/mysqlinfo.library.choosing.php)，是PHP语言编译时的决定，一旦PHP编译完成以后，要更改估计比较困难（我没有尝试过，因此不太肯定）。

### 2.2 libmysqlclient ###

这是一个根据 MySQL client/server 协议，使用C语言实现的库。有很多的客户端api使用libmysqlclient这个库去和MySQL Server进行通信(Exceptions are except Connector/J and Connector/Net.)。 

### 2.3 mysqlnd ###

MySQL Native Driver实现和libmysqlclient同样的功能。但MySQL Native Driver是PHP 5.3.0 官方的代码。

mysqlnd 和 libmysqlclient最大的不同是，mysqlnd 针对与PHP的应用交互进行优化，而libmysqlclient是早期为C应用程序设计的，并没有针对性的优化。

另外，mysqlnd 可以支持很多高级的特性，比如**prepared语句支持**（曾经在这个prepare的问题上被坑过，当时用的正是libmysqlclient）。

### 2.4 性能对比 ###

更加详细的对比，移步博文[Benchmark: libmysql vs mysqlnd](https://usu.li/benchmark-libmysql-vs-mysqlnd/)