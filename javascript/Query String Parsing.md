##1.    URL encoding

为什么要进行URL encoding？这是因为，有些字符是不能成为URL一部分的，举个例子，比如空格符。另外，有些有特殊含义的保留字符，比如#，作为HTML锚点，用于定位到HTML文档的某个位置上；=符号在URL里用于分割URL参数的key和value。

URL encoding依据以下规则：

-    字母（A–Z 以及 a–z），数字（0-9）以及'.'，'-'，'~'和'_'这些字符不进行编码
-    空格符要编码成+或者"%20"
-    所有其他的字符，要被编码成%HH这样形式的[十六进制](http://en.wikipedia.org/wiki/Hexadecimal)表示；任何非ASCII字符，应该要取UTF-8的十六进制（或者是其他编码），以%HH表示；

>NOTE:  更多详细信息，可以参考这篇WIKI——[Query String](http://en.wikipedia.org/wiki/Query_string)。关于空格符以及其他的保留字符，可以去查阅标准文档[RFC 1738](http://tools.ietf.org/html/rfc1738)。

##2.    Javascript Encode/Decode Functions

Javascript内置了几对编码和解码的函数。起初只有`escape`和`unescape`这一对方法，但后来这对方法已经不推荐使用了，新的标准制定了两对新的编码和解码函数：`encodeURI` 和 `decodeURI` 以及 `encodeURIComponent` 和 `decodeURIComponent`。

但实际上内置的编码解码函数，对于URL query string的编码和解码却不是十分正确的。

代码                         | 结果             | 说明               |
----------------------------|-----------------|--------------------|
"A + B"                     | "A+%2B+B"       | 期望值              |
escape("A + B")             | "A%20+%20B"     | 错误               |    
encodeURI("A + B")          | "A%20+%20B"     | 错误               |
encodeURIComponent("A + B") | "A%20%2B%20B"   | 可以接受，但是有点奇怪 |

代码                           | 结果           | 说明               |
------------------------------|---------------|--------------------|
"A+%2B+B"                     | "A + B"       | 期望值              |
unescape("A+%2B+B")           | "A+++B"       | 错误               |    
decodeURI("A+%2B+B")          | "A+%2B+B"     | 错误               |
decodeURIComponent("A+%2B+B") | "A+++B"       | 错误               |


>NOTE:SEE ALSO:[Javascript Madness: Query String Parsing](http://unixpapa.com/js/querystring.html)