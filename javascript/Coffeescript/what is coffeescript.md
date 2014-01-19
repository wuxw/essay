#CoffeeScript 是什么？#

[Coffeescript](http://coffeescript.org/)是一门可以编译成javascript的语言。

它的语法设计收到来自于Ruby和Python的启发，并且实现了许多这两门语言的特性。

CoffeeScript编写的代码非常简洁，它使用代码缩进来识别代码块，另外语言层面提供的一些特性，比如class extends mixin map等，都会让你的编码量大幅度下降，比起直接使用javascript来编写代码要优雅很多。

可能你会担心你不能在CoffeeScript引用其他使用js编写的库。不必担心，CoffeeScript并不是js的超集，你大可以在CoffeeScript代码里使用这些库。

实际上，想要使用CoffeeScript，你依然需要理解js。前面也说过了，CoffeeScript最后会编译成为js，代码依然运行在js runtime。debug的时候你需要能够理解引起错误的js代码才行。

正像如今js在nodejs的环境下，可以运行在服务端一样，CoffeeScript也不仅仅只限于运行在浏览器客户端，它一样可以运行在nodejs之上。

#快速入门#

CoffeeScript提供了两种编译方式，一种是基于浏览器编译的方式，另外一种则是建立在nodejs的基础上。

**browser-based**

    <script src="http://jashkenas.github.com/coffee-script/extras/coffee-script.js" type="text/javascript" charset="utf-8"></script>
    <script type="text/coffeescript">
      # Some CoffeeScript
    </script>

**nodejs-based**

    npm install -g coffee-script
    coffee --compile my-script.coffee

如果nodejs版编译器的--output参数没有指定，默认情况下，代码会被编译成同名文件，文件后缀则会改成.js。