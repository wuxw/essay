##数组直接量##

    array1 = [1, 2, 3]

在coffeescript中，数组还有一些很有意思的地方，比如我可以用下面的方式定义一个范围数组：

    range = [1..5]

而最后它会被编译成：

    var range;
    range = [1, 2, 3, 4, 5];

还有更有趣的地方，我可以使用类似的语法去操作数组，比如：

    firstTwo = ["one", "two", "three"][0..1]
    numbers = [0..9]
    numbers[3..5] = [-3, -4, -5]

##数组遍历##

也许看到这里，你会想，应该也有更简单的方式去遍历一个数组吧，就像我写js那样，使用for循环语句。是的，我们当然有：

    words = ["rattled", "roudy", "rebbles", "ranks"]
    for item, i in words
        # item = words[i]
        # do something

ES5中，数组还添加了一个新的API——[forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)：

    array.forEach(function(item, i){
      myFunction(item)
    });

在coffeescript中，你可以更优雅：

    myFunction(item) for item in array

看上去很直观，也更加口语化，就像是你在写文章一样，不是吗？

##数组的其他惯常用法##

当然，对于数组而且，还有一些其他惯用的操作，类似ES5 Array的新API——[map](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Array/map)：

    var result = []
    for (var i=0; i < array.length; i++)
      result.push(array[i].name)
    
    //  ES5 Array的新API——map
    var result = array.map(function(item, i){
      return item.name;
    });

你大可不必如此繁琐：

    result = (item.name for item in array)

如果我希望能从一个数组中，根据一定条件去筛选某一个项，该怎么做？使用JS，你会这么做：
    
    var result = []
    for (var i=0; i < array.length; i++)
      if (array[i].name == "test")
        result.push(array[i])
    
    //  ES5 Array的新API——filter
    result = array.filter(function(item, i){
      return item.name == "test"
    });

哦哦，你瞧，我们又认识了一个ES5的API，就是[filter](https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/array/filter)。其实不是说这些新api不好，不过使用这些API会带来一次额外的API调用，多少会对性能有一些不好的影响。幸运的是，coffeescript提供类似的方式，但本质上却使用更快的for循环去实现：
    
    #   注意这边when的用法
    result = (item for item in array when item.name is "test")

数组另外一个最常用的操作，估计就是检查是否含有某一个值了。我们可以使用indexOf方法来做，但一些低版本的IE浏览器尚且不支持这个函数。

    var included = (array.indexOf("test") != -1)

coffeescript中我们使用in关键字：

    included = "test" in array

这段代码最后被翻译成：

    var included;
    var __indexOf = Array.prototype.indexOf || function(item) {
      for (var i = 0, l = this.length; i < l; i++) {
        if (this[i] === item) return i;
      }
      return -1;
    };
    included = __indexOf.call(array, "test") >= 0;

完美兼容IE。