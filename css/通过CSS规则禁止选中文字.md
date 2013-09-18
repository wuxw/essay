##前言##

禁止选中文字在某些场景下还是有必要的，比如不想让他人复制自己的文章之类的。这时候我们可以通过使用CSS+JS来解决这一问题。另外，这边要指出的是，user-select目前还不是W3C的正式标准，各个浏览器都是以私有属性的方式提供支持。

##语法##

	Formal syntax: none | text | all | element

	(-prefix-)user-select: none;
	(-prefix-)user-select: text;
	(-prefix-)user-select: all;
	(-prefix-)user-select: element;

##示例##

	.row-of-icons {
		-webkit-user-select: none;  /* Chrome all / Safari all */
		-moz-user-select: none;     /* Firefox all */
		-ms-user-select: none;      /* IE 10+ */
		
		/* No support for these yet, use at own risk */
		-o-user-select: none;
		user-select: none;          
	}

##IE兼容性##

目前在IE 10以及IE 10以上版本的浏览器可以使用-ms-user-select这个规则，但在更早版本的IE，我们只能通过javascript实现禁止选中文本：

	$(el).attr('unselectable','on') 
	.css({'-moz-user-select':'-moz-none', 
		'-moz-user-select':'none', 
		'-o-user-select':'none', 
		'-khtml-user-select':'none', /* you could also put this in a class */ 
		'-webkit-user-select':'none',/* and add the CSS class here instead */ 
		'-ms-user-select':'none', 
		'user-select':'none' 
	}).bind('selectstart', function(){ 
		return false; 
	}); 

##参考文档##

1.	[MDN user-select](https://developer.mozilla.org/en-US/docs/Web/CSS/user-select)
2.	[user-select](http://css-tricks.com/almanac/properties/u/user-select/)
3.	[禁止选中文字兼容IE、Chrome、FF等](http://www.jb51.net/article/41127.htm)
4.	[How can I prevent the selection of text in IE?](http://stackoverflow.com/questions/6100692/how-can-i-prevent-the-selection-of-text-in-ie)