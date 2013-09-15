##术语##

1.	__UI events__: 用户接口事件，这些事件是由外设（比如鼠标，键盘）触发的。
1.	__UI Logical events__: 设备无关的用户接口事件，比如focus事件。
1.	__Mutation events__: 变动事件。这些事件在文档结构发生改变的时候触发。
1.	__Capturing__: 捕捉，即是事件在目标DOM节点处理之前，由事件目标前驱的事件处理程序处理。
1.	__Bubbling__: 捕捉，即是事件在目标DOM节点处理之后，由事件目标前驱的事件处理程序处理。
1.	__Cancelable__: 指示是否阻止DOM实现指定的默认事件处理程序处理。

##事件流##

###基础###

每一个Event事件对象都有一个EventTarget属性，这个属性是一个DOM节点的引用。当事件到达目标DOM节点，在这个DOM节点注册的任何事件处理程序都会被触发。事件处理程序的触发顺序是不确定的。

事件流在事件的所有处理程序都执行完成之后才算结束。当然，如果启用了capture（事件捕捉）或者bubbling（事件冒泡）的话，事件流还是可以被修改的。

在事件流的执行过程中，任何事件处理程序抛出异常，整个事件流都将停止。

![Event capture && Event bubbling](./evt-capture-bubbling.jpg)

###Event capture（事件捕捉）###

事件捕捉的处理流程是从文档树根节点，一直向下处理，直到目标节点才停止。

这里要注意的是，调用Event接口的stopProgagation方法会组织事件流的后续处理。

###Event bubbling（事件冒泡）###

事件冒泡是从目标节点先开始出来，然后顺着目标节点的父节点，一级一级往上处理，知道文档树根节点。

这里要注意的是，调用Event接口的stopProgagation方法会组织事件流的后续处理。

###Event cancelation（事件取消）###

有些事件是可以取消的，因为这些事件，DOM实现会生成默认的事件处理程序。一个例子就是web浏览器内的超链接。

一个或者多个事件处理程序调用Event接口的preventDefault方法就能取消事件的默认处理程序。

##接口##

###EventTarget###

	interface EventTarget {
	  void               addEventListener(in DOMString type, 
	                                      in EventListener listener, 
	                                      in boolean useCapture);
	  void               removeEventListener(in DOMString type, 
	                                         in EventListener listener, 
	                                         in boolean useCapture);
	  boolean            dispatchEvent(in Event evt)
	                                        raises(EventException);
	};

这边值得说明的是dispatchEvent方法。通过这个方法我们可以手工触发w3c的标准标准事件或者自定义事件。

###Event###

	// Introduced in DOM Level 2:
	interface Event {
	  // PhaseType
	  const unsigned short      CAPTURING_PHASE                = 1;
	  const unsigned short      AT_TARGET                      = 2;
	  const unsigned short      BUBBLING_PHASE                 = 3;
	
	  readonly attribute DOMString        type;
	  readonly attribute EventTarget      target;
	  readonly attribute EventTarget      currentTarget;
	  readonly attribute unsigned short   eventPhase;
	  readonly attribute boolean          bubbles;
	  readonly attribute boolean          cancelable;
	  readonly attribute DOMTimeStamp     timeStamp;
	  void               stopPropagation();
	  void               preventDefault();
	  void               initEvent(in DOMString eventTypeArg, 
	                               in boolean canBubbleArg, 
	                               in boolean cancelableArg);
	};

###EventException###

	// Introduced in DOM Level 2:
	exception EventException {
	  unsigned short   code;
	};
	// EventExceptionCode
	const unsigned short      UNSPECIFIED_EVENT_TYPE_ERR     = 0;

###DocumentEvent###

	// Introduced in DOM Level 2:
	interface DocumentEvent {
	  Event              createEvent(in DOMString eventType)
	                                        raises(DOMException);
	};

createEvent接口返回一个Event对象，然后通过dispatchEvent方法分发事件，事件内部的相应的初始化方法会被调用，对事件对象进行初始化，之后就是按照事件流分发和处理事件。

示例：

	var evt = document.createEvent( 'uiEvt' )

###UIEvent###

	// Introduced in DOM Level 2:
	interface UIEvent : Event {
	  readonly attribute views::AbstractView  view;
	  readonly attribute long             detail;
	  void               initUIEvent(in DOMString typeArg, 
	                                 in boolean canBubbleArg, 
	                                 in boolean cancelableArg, 
	                                 in views::AbstractView viewArg, 
	                                 in long detailArg);
	};

所有事件在dispatchEvent后都会调用initUIEvent对Event事件对象进行初始化。

UIEvent包括：

1.	__DOMFocusIn__
2.	__DOMFocusOut__	
3.	__DOMActivate__

>NOTE：这几个事件日常开发并不常用的感觉。当然，我们可以做一个实验，就是关于DOMFocusIn focus DOMFocusOut blur 以及 DomActivate 事件的触发顺序。

	<input type="text" id="t">

    <script type="text/javascript">
	    function onMouseDown (argument) {
	        console.log( 'mouse down' );
	    };
	    function onClick (argument) {
	        console.log( 'click' );
	    };
	    function onFocusIn (argument) {
	        console.log( 'focus in ' );
	    };
	    function onFocus (argument) {
	        console.log( 'focus' );
	    };
	    function onFocusOut (argument) {
	        console.log( 'focus out' );
	    };
	    function onBlur (argument) {
	        console.log( 'blur' );
	    };
	    function onActive (argument) {
	        console.log( 'dom active and argument.detail is ' + argument.detail );
	    };
	
	    var input = document.getElementById('t');
	    input.addEventListener( 'DOMFocusIn',onFocusIn );
	    input.addEventListener( 'focus',onFocus );
	    input.addEventListener( 'DOMFocusOut',onFocusOut );
	    input.addEventListener( 'mousedown',onMouseDown );
	    input.addEventListener( 'click',onClick );
	    input.addEventListener( 'blur',onBlur );
	    input.addEventListener( 'DOMActivate',onActive );
    </script>

这段代码执行后的结果就是：

	mouse down 
	focus 
	focus in  
	click 
	dom active and argument.detail is 1 
	dom active and argument.detail is 1 
	blur 
	focus out 

###MouseEvent###

	// Introduced in DOM Level 2:
	interface MouseEvent : UIEvent {
	  readonly attribute long             screenX;
	  readonly attribute long             screenY;
	  readonly attribute long             clientX;
	  readonly attribute long             clientY;
	  readonly attribute boolean          ctrlKey;
	  readonly attribute boolean          shiftKey;
	  readonly attribute boolean          altKey;
	  readonly attribute boolean          metaKey;
	  readonly attribute unsigned short   button;
	  readonly attribute EventTarget      relatedTarget;
	  void               initMouseEvent(in DOMString typeArg, 
	                                    in boolean canBubbleArg, 
	                                    in boolean cancelableArg, 
	                                    in views::AbstractView viewArg, 
	                                    in long detailArg, 
	                                    in long screenXArg, 
	                                    in long screenYArg, 
	                                    in long clientXArg, 
	                                    in long clientYArg, 
	                                    in boolean ctrlKeyArg, 
	                                    in boolean altKeyArg, 
	                                    in boolean shiftKeyArg, 
	                                    in boolean metaKeyArg, 
	                                    in unsigned short buttonArg, 
	                                    in EventTarget relatedTargetArg);
	};

Mouse包括：

1.	__click__: 在用户单击主鼠标按钮或者按下回车键时触发	
1.	__mousedown__: 在用户按下任意鼠标按钮时触发	
1.	__mouseup__: 在用户释放鼠标按钮时触发	
1.	__mouseover__: 在鼠标指针位于一个元素外部，而后用户将其移入另一个元素内时触发
1.	__mousemove__: 当鼠标指针在元素内部移时重复地触发
1.	__mouseout__: 在鼠标指针位于一个元素上方，而后用户将其移入另一个元素时触发

页面上所有元素都支持鼠标事件，所有鼠标事件都会冒泡，也可以被取消，而取消鼠标事件将会影响浏览器的默认行为。

虽然鼠标事件主要使用鼠标来触发，但在按下鼠标时键盘上的某些键的状态也可以影响到所要采取的操作。这些修改键就是__Shift__、__Ctrl__、__Alt__和__Meta__，它们经常被用来修改鼠标事件的行为。DOM为此规定了4个属性，表示这些修改键的状态：__shiftKey__、__ctrlKey__、__altKey__和__metaKey__。如果相应的键被按下了，则值为true，否则值为false。

只有在主鼠标按钮被单击时才会触发click事件，但是对于mousedown和mouseup事件，其event对象存在一个button属性，表示按下或释放的按钮：	

+	0 表示主鼠标按钮
+	1 表示中间滚轮按钮
+	2 表示次鼠标按钮

>NOTE: IE中的button属性与DOM的button属性有[很大差异](http://www.quirksmode.org/js/events_properties.html#button)。

>+	0: 表示没有按下按钮。
>+	1: 表示按下了主鼠标按钮。
>+	2: 表示按下了次鼠标按钮。
>+	3: 表示同时按下了主、次鼠标按钮。
>+	4: 表示按下了中间鼠标按钮。
>+	5: 表示同时按下了主鼠标按钮和中间的鼠标按钮。
>+	6: 表示同时按下了次鼠标按钮和中间的鼠标按钮。
>+	7: 表示同时按下了三个鼠标按钮。

###Key events###

DOM2标准并没有提供任何关于键盘事件的标准。不过我们日常开发过程中，会用到三个键盘事件，分别是：

1.	__keydown__: 当用户按下键盘上的任意键时触发，如果按住不放会重复触发此事件
2.	__keypress__: 当用户按下键盘上的字符键时触发，如果按住不放会重复触发此事件
3.	__keyup__: 当用户释放键盘上的键时触发

>NOTE:	Firefox、Chrome和Safari的event对象都支持一个__charCode__属性，这个属性只有在发生__keypress事件时才包含值__，而且这个值是按下的那个键所代表字符的ASCII编码。IE和Opera则是在__keyCode__中保存字符的ASCII编码。

###MutationEvent###

	// Introduced in DOM Level 2:
	interface MutationEvent : Event {
	  // attrChangeType
	  const unsigned short      MODIFICATION                   = 1;
	  const unsigned short      ADDITION                       = 2;
	  const unsigned short      REMOVAL                        = 3;
	
	  readonly attribute Node             relatedNode;
	  readonly attribute DOMString        prevValue;
	  readonly attribute DOMString        newValue;
	  readonly attribute DOMString        attrName;
	  readonly attribute unsigned short   attrChange;
	  void               initMutationEvent(in DOMString typeArg, 
	                                       in boolean canBubbleArg, 
	                                       in boolean cancelableArg, 
	                                       in Node relatedNodeArg, 
	                                       in DOMString prevValueArg, 
	                                       in DOMString newValueArg, 
	                                       in DOMString attrNameArg, 
	                                       in unsigned short attrChangeArg);
	};

变动事件包括以下不同事件类型：

1.	__DOMSubtreeModified__: 在DOM结构中发生任何变化时触发
1.	__DOMNodeInserted__: 在一个节点作为子节点被插入到另一个节点中时触发
1.	__DOMNodeRemoved__:	在节点从其父节点中被移除时触发
1.	__DOMNodeRemovedFromDocument__:	 在一个节点被直接从文档中移除或通过子树间接从文档中移除之前触发
1.	__DOMNodeInsertedIntoDocument__:	在一个节点被直接插入文档或通过子树间接插入文档之后触发
1.	__DOMAttrModified__:	在属性被修改之后触发
1.	__DOMCharacterDataModified__:	在文本节点的值发生变化时触发

###HTML event###

HTML event是HTML4.0带来的事件，以及支持[DOM LEVEL 0](http://www.w3.org/TR/2000/REC-DOM-Level-2-Events-20001113/glossary.html#dt-DOM-Level-0)的浏览器支持的标准事件。

>NOTE:要创建一个HTML event定义事件Event对象，使用'HTMLEvents'作为DocumentEvent.createEvent方法的参数。	

	//	Event {clipboardData: undefined, cancelBubble: false, returnValue: true, srcElement: null, defaultPrevented: false…}
	var event = document.createEvent( 'HTMLEvents' )
	//	NotSupportedError: The implementation did not support the requested type of object or operation.
	var event = document.createEvent( 'load' )

HTML event包括以下不同事件类型：

1.	__load__	
1.	__unload__	
1.	__abort__	
1.	__error__: 这个事件在image加载失败的时候触发，不过现在也支持OBJECT标签，BODY标签以及FRAMESET。	
1.	__select__: 文本域中选中文本的时候触发，只有INPUT以及TEXTAREA标签支持。
1.	__change__: 只有INPUT，SELECT以及TEXTAREA标签支持。	
1.	__submit__: 只有FORM标签支持。	
1.	__reset__: 只有FORM标签支持。	
1.	__focus__: 只有LABEL, INPUT, SELECT, TEXTAREA, and BUTTON标签支持。
1.	__blur__: 只有LABEL, INPUT, SELECT, TEXTAREA, and BUTTON标签支持。
1.	__resize__	
1.	__scroll__

##参考文档##

1.	[Document Object Model Events](http://www.w3.org/TR/2000/REC-DOM-Level-2-Events-20001113/events.html)
2.	[JavaScript 中的事件模拟](http://www.cnblogs.com/zoho/archive/2013/03/30/2990442.html)
3.	[浅谈DOM事件的优化](http://stylechen.com/dom-event-optimize.html)
4.	[[译]什么是Shadow Dom](http://www.toobug.net/article/what_is_shadow_dom.html)
5.	[JavaScript并行运算新机遇——Web Workers的神奇魔法](http://www.ituring.com.cn/article/5917)
6.	[事件模型在各浏览器中存在差异](http://www.w3help.org/zh-cn/causes/SD9011)
7.	[event.button](https://developer.mozilla.org/zh-CN/docs/DOM/event.button)
8.	[[JavaScript]事件](http://hanviseas.blog.51cto.com/5400240/1034837)