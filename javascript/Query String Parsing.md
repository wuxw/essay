##1.    URL encoding

Some characters cannot be part of a URL (for example, the space) and some other characters have a special meaning in a URL: for example, the character # can be used to further specify a subsection (or fragment) of a document; the character = is used to separate a name from a value. A query string may need to be converted to satisfy these constraints. This can be done using a schema known as [URL encoding](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters).

In particular, encoding the query string uses the following rules:

-    Letters (A¨CZ and a¨Cz), numbers (0¨C9) and the characters '.','-','~' and '_' are left as-is
-    SPACE is encoded as '+' or "%20" 
-    All other characters are encoded as %HH [hex](http://en.wikipedia.org/wiki/Hexadecimal) representation with any non-ASCII characters first encoded as UTF-8 (or other specified encoding)
The octet corresponding to the tilde ("~") character is often encoded as "%7E" by older URI processing implementations; the "%7E" can be replaced by "~" without changing its interpretation.

The encoding of SPACE as '+' and the selection of "as-is" characters distinguishes this encoding from [RFC 1738](http://tools.ietf.org/html/rfc1738).

>NOTE: For more, you can read this WIKI--[Query String](http://en.wikipedia.org/wiki/Query_string)

##2.    Javascript Encode/Decode Functions

http://unixpapa.com/js/querystring.html

```
var arr=[];
for(var i=0;i<256;i++){
	var char=String.fromCharCode(i);
	if(encodeURI(char)!== encodeURIComponent(char)){
		arr.push({
			character:char,
			encodeURI:encodeURI(char),
			encodeURIComponent:encodeURIComponent(char)
		})
	}
}
console.table(arr);
```