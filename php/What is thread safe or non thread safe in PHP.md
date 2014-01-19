【原文】[What is thread safe or non thread safe in PHP](http://stackoverflow.com/questions/1623914/what-is-thread-safe-or-non-thread-safe-in-php)

##Needed background on Concurrency approaches:##

Different web servers implement different techniques for handling incoming HTTP requests in parallel. A pretty popular technique is using Threads -- that is, the web server will create/dedicate a single thread for each incoming request. The Apache HTTP web server supports multiple models for handling requests, one of which (called the Worker MPM) uses Threads. But it supports another concurrency model called the Prefork MPM which uses Processes -- that is, the web server will create/dedicate a single process for each request.

There are also other completely different concurrency models (using Asynchronous sockets/IO), as well as ones that mix two or even three models together. For the purpose of answering this question, we are only concerned with the two models above, and taking Apache HTTP server as an example.

##Needed background on how PHP "integrates" with web servers:##

PHP itself does not respond to the actual HTTP requests -- this is the job of the web server. So what we do, is configure the web server to forward requests to PHP for processing, then receive the result and send it back to the user. There are multiple ways to chain the web server with PHP. For Apache HTTP Server, the most popular is "mod_php". This module is actually PHP itself but compiled as a module for the web server, and so it gets loaded right inside it.

There are other methods for chaining PHP with Apache and other web servers, but mod_php is the most popular one and will also serve for answering your question.

You may not have needed to understand these details before, because hosting companies and GNU/Linux distros come with everything prepared for us.

##Now, onto your question!##

Since with mod_php, PHP gets loaded right into Apache, if Apache is going to handle concurrency using its Worker MPM (that is, using Threads) then PHP must be able to operate within this same multi-threaded environment -- meaning, PHP has to be thread-safe to be able to play ball correctly with Apache!

At this point, you should be thinking "Ok, so if I'm using a multi-threaded web server and I'm going to embed PHP right into it, then I must use the thread-safe version of PHP". And this would be correct thinking. However, as it happens, PHP's thread-safety is highly disputed. It's a use-if-you-really-really-know-what-you-are-doing ground.

##Final notes##

In case you are wondering, my personal advice would be to not use PHP in a multi-threaded environment if you have the choice!

Speaking only of UNIX-based environments, I'd say that fortunately, you only have to think of this if you are going to use PHP with Apache web server, in which case you are advised to go with the Prefork MPM of Apache (which doesn't use threads, and therefore, PHP thread-safety doesn't matter) and all GNU/Linux distros that I know of will take that decision for you when you are installing Apache + PHP through their package system, without even prompting you for a choice. If you are going to use other webservers such as nginx or lighttpd, you won't have the option to embed PHP into them anyway. You will be looking at using FastCGI or something equal which works in a different model where PHP is totally outside of the web server with multiple PHP processes used for answering requests through e.g. FastCGI. For such cases, thread-safety also doesn't matter.

If you also look at the Command Line version of PHP -- thread safety does not matter.

Finally, if thread-safety doesn't matter so which version should you use -- the thread-safe or the non-thread-safe? Frankly, I don't have a scientific answer! But I'd guess that the non-thread-safe version is faster and/or less buggy, or otherwise they would have just offered the thread-safe version and not bothered to give us the choice!

##参考文档##

1.	[Difference between PHP thread safe and non thread safe binaries](http://www.iis-aid.com/articles/my_word/difference_between_php_thread_safe_and_non_thread_safe_binaries)
2.	[PHP版本VC6与VC9、Thread Safe与None-Thread Safe等的区别](http://down.chinaz.com/server/201111/1329_1.htm)