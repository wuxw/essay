##函数声明##

coffeescript声明函数很有特色，你不需要繁琐的输入function语句，取而代之，你直接使用->符号。

函数可以是一行代码或者多行代码，coffeescript会隐式return函数最后的表达式。也就是说你无须刻意去return，除非你需要提早return。

示例：
    func = () -> "bar"
会被编译成：
    var func;
    func = function() {
      return "bar";
    };

##函数参数##

示例：

    times = (a, b) -> a * b

coffeescript允许我们指定函数参数的默认值，你可以这么声明一个函数：

    times = (a = 1, b = 2) -> a * b
最后代码会编译成：

    var times;
    times = function(a, b) {
      if (a == null) {
        a = 1;
      }
      if (b == null) {
        b = 2;
      }
      return a * b;
    };

coffeescript还允许你声明多个参数，使用...标记：

    sum = (nums...) -> 
    result = 0
    nums.forEach (n) -> result += n
    result

这个例子中，nums是一个数组，而不是arguments那样的array-like的变量。也就是coffeescript默认帮你调用了Array.prototype.slice方法获取了函数参数的数组了。

##函数调用##

示例：

    alert inspect a
    alert inspect(a)

当你要调用的函数不传任何参数的时候，最好是加上圆括号以免出错。

##函数上下文##

这边说的其实是js中的this引用的问题。一个很典型的场景就是dom事件处理程序。在事件处理程序中，this是指向出发这个事件的dom。

典型的做法如下：

    var me = this;

但在coffeescript，你也可以这么做：

    element.addEventListener "click", (e) => this.clickHandler(e)

原本我们声明一个函数使用->符号，这边换成=>即可。这有点类似[ES5的bind方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)