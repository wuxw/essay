##术语##

__UI events__

	用户接口事件，这些事件是由外设（比如鼠标，键盘）触发的。

__UI Logical events__	

	设备无关的用户接口事件，比如focus事件。

__Mutation events__	

	文档结构变化事件。这些事件在文档结构发生改变的时候触发。

__Capturing__	

	捕捉，即是事件在目标DOM节点处理之前，由事件目标前驱的事件处理程序处理。

__Bubbling__	

	捕捉，即是事件在目标DOM节点处理之后，由事件目标前驱的事件处理程序处理。

__Cancelable__	

	指示是否阻止DOM实现指定的默认事件处理程序处理。

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

__DOMFocusIn__	

__DOMFocusOut__	

__DOMActivate__

>NOTE:编写DEMO以及做更多的尝试

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

__click__	

__mousedown__	

__mouseup__	

__mouseover__	

__mousemove__	

__mouseout__

###Key events###

DOM2标准并没有提供任何关于键盘事件的标准。

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

>NOTE:编写代码测试，以及相应的浏览器兼容性

文档变化事件包括以下不同事件类型：

__DOMSubtreeModified__	

__DOMNodeInserted__	

__DOMNodeRemoved__	

__DOMNodeRemovedFromDocument__	

__DOMNodeInsertedIntoDocument__	

__DOMAttrModified__	

__DOMCharacterDataModified__

###HTML event###

HTML event是HTML4.0带来的事件，以及支持[DOM LEVEL 0](http://www.w3.org/TR/2000/REC-DOM-Level-2-Events-20001113/glossary.html#dt-DOM-Level-0)的浏览器支持的标准事件。

>NOTE:要创建一个HTML event定义事件Event对象，使用'HTMLEvents'作为DocumentEvent.createEvent方法的参数。	

	//	Event {clipboardData: undefined, cancelBubble: false, returnValue: true, srcElement: null, defaultPrevented: false…}
	var event = document.createEvent( 'HTMLEvents' )
	//	NotSupportedError: The implementation did not support the requested type of object or operation.
	var event = document.createEvent( 'load' )

HTML event包括以下不同事件类型：

__load__	

__unload__	

__abort__	

__error__	

	这个事件在image加载失败的时候触发，不过现在也支持OBJECT标签，BODY标签以及FRAMESET。	

__select__	

	文本域中选中文本的时候触发，只有INPUT以及TEXTAREA标签支持。

__change__	

	只有INPUT，SELECT以及TEXTAREA标签支持。	

__submit__	

	只有FORM标签支持。	

__reset__	

	只有FORM标签支持。	

__focus__	

	只有LABEL, INPUT, SELECT, TEXTAREA, and BUTTON标签支持。

__blur__	

	只有LABEL, INPUT, SELECT, TEXTAREA, and BUTTON标签支持。

__resize__	

__scroll__