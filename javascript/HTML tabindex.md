##定义##

tabindex指定HTML元素的tab顺序。

##tabindex在HTML 4.01和 HTML5 的区别##

在HTML5里，任何元素都可以指定tabindex（ 不过我觉得没有必要这么做就是了 ）。而在HTML4里，只有&lt;a&gt;，&lt;area&gt;， &lt;button&gt;，&lt;input&gt;，&lt;object&gt;，&lt;select&gt;和&lt;textarea&gt;支持tabindex。

##tabindex的使用##

+	默认的tabIndex属性为 0 ，将排列在在所有指定tabIndex的控件之后
+	把tabIndex属性设为一个负值（如tabIndex="-1"），那么这个链接将被排除在TAB键的序列之外
+	如果有两个控件的tabIndex属性相同，则以控件在html代码中出现的顺序为准
+	tabIndex的值可为0至32767之间的任意数字
+	要启用tabIndex，首先，元素必须是focusable的

##Enter as Tab##

在一些应用场景下，我们可能需要让enter键按下去的时候表现得和tab键按下去一样，特别是在企业应用中需要填写大量表单的情况下，这个功能是可以大幅度提高输入效率的。

我们可以使用keydown来实现这个功能：

	$('body').on('keydown', 'input, select, textarea', function(e) {
	    var self = $(this)
	      , form = self.parents('form:eq(0)')
	      , focusable
	      , next
	      ;
	    if (e.keyCode == 13) {
	        focusable = form.find('input,a,select,button,textarea').filter(':visible');
	        next = focusable.eq(focusable.index(this)+1);
	        if (next.length) {
	            next.focus();
	        } else {
	            form.submit();
	        }
	        return false;
	    }
	});

##参考链接##

1.	[Web 2.0 技术中的可访问性](http://www.ibm.com/developerworks/cn/web/wa-aj-web20/)
2.	[Keyboard Accessibility](http://webaim.org/techniques/keyboard/)
3.	[HTML tabIndex属性与EVENT焦点事件的blur和focus](http://www.ipmtea.net/javascript/201101/06_421.html)
4.	[Focus, tabIndex and behavior of browsers](http://nemisj.com/focusable/)
5.	[Tabbing navigation](http://www.w3.org/TR/1999/REC-html401-19991224/interact/forms.html#adef-tabindex)