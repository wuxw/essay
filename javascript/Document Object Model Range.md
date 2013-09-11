Range接口的完整API描述请参考W3C文档[《Document Object Model Range》]([Rnage](http://www.w3.org/TR/DOM-Level-2-Traversal-Range/ranges.html#Level-2-Range-idl))

##术语##

###Position###

+	一个Range对象包含两个边界点（boundary-points），每个边界点的通过一个节点（node）和偏移量（offset）来唯一定位。
+	如果容器（node）刚好是Attr，Document，DocumentFragment，Element或者EntityReference节点， 偏移量（offset）位于容器子节点的索引区间。
+	如果容器（node）是CharacterData，Comment或者ProcessingInstruction节点，那么偏移量（offset）就是文本（UTF-16编码）字符的索引。
+	如果容器（node）必须是Element，Comment，ProcessingInstruction，EntityReference，CDATASection，Document，DocumentFragment， Attr，或者Text节点的一种。 

![Range Example](http://www.w3.org/TR/DOM-Level-2-Traversal-Range/images/RangeExample.gif)

###Selection and Partial Selection###

+	如果一个节点或者16bit单位编码的文本位于Range对象的两个边界点支架，我们称为选中（selected）。

>NOTE:	如上图所示，Range2选中了P节点，Range 3选中了text节点“Blah xyz”。

+	如果一个节点包含Range对象的一个边界点，那么这个节点被Range半选（partially selected）。

>NOTE:	如上图所示，Range1就是半选的情况。

##Creating a Range##

__[DocumentRange](http://www.w3.org/TR/DOM-Level-2-Traversal-Range/ranges.html#Level-2-DocumentRange-idl)接口__

	interface DocumentRange {
		Range createRange();
	}

 >NOTE:	createRange返回一个包含默认值的Range对象。默认情况下，这个Range对象的两个边界点node都是Document节点，并且offset值都是0。

###Changing a Range's Position###

可以通过Range.setStart和Range.setEnd两个方法指定Range对象的位置：

	void setStart(in Node parent, in long offset) 
					raises(RangeException);
	void setEnd(in Node parent, in long offset)	
					raises(RangeException);

It is also possible to set a Range's position relative to nodes in the tree:

	void setStartBefore(in Node node);
                        	raises(RangeException);
	void setStartAfter(in Node node);
                       		raises(RangeException);
	void setEndBefore(in Node node);
                      		raises(RangeException);
	void setEndAfter(in Node node);
                     		raises(RangeException);

A Range can be collapsed to either boundary-point:
	
	void collapse(in boolean toStart);

Passing TRUE as the parameter toStart will collapse the Range to its start, FALSE to its end.

The following methods can be used to make a Range select the contents of a node or the node itself.

	void selectNode(in Node n);
	void selectNodeContents(in Node n);

The following examples demonstrate the operation of the methods selectNode and selectNodeContents:

	Before:
	  ^<BAR><FOO>A<MOO>B</MOO>C</FOO></BAR>
	After Range.selectNodeContents(FOO):
	  <BAR><FOO>A<MOO>B</MOO>C</FOO></BAR>
	(In this case, FOO is the parent of both boundary-points)
	After Range.selectNode(FOO):
	
	<BAR><FOO>A<MOO>B</MOO>C</FOO></BAR>

##Comparing Range Boundary-Points##

##Deleting Content with a Range##

One can delete the contents selected by a Range with:

	void deleteContents();

Some examples : 

	(1) <FOO>AB<MOO>CD</MOO>CD</FOO>	-->	<FOO>A^CD</FOO>
	(2) <FOO>A<MOO>BC</MOO>DE</FOO>		-->		<FOO>A<MOO>B</MOO>^E</FOO>
	(3) <FOO>XY<BAR>ZW</BAR>Q</FOO>		-->		<FOO>X^<BAR>W</BAR>Q</FOO>
	(4) <FOO><BAR1>AB</BAR1><BAR2/><BAR3>CD</BAR3></FOO>	-->  <FOO><BAR1>A</BAR1>^<BAR3>D</BAR3>

After deleteContents() is invoked on a Range, the Range is collapsed.

##Extracting Content##

If the contents of a Range need to be extracted rather than deleted, the following method may be used:

	 DocumentFragment extractContents();

Some examples : 

	(1) <FOO>AB<MOO>CD</MOO>CD</FOO>  -->	B<MOO>CD</MOO>
	(2) <FOO>A<MOO>BC</MOO>DE</FOO>  -->		<MOO>C<MOO>D
	(3) <FOO>XY<BAR>ZW</BAR>Q</FOO>  -->		Y<BAR>Z</BAR>
	(4) <FOO><BAR1>AB</BAR1><BAR2/><BAR3>CD</BAR3></FOO> -->		<BAR1>B</BAR1><BAR2/><BAR3>C</BAR3>

##Cloning Content##

##Inserting Content##

##Surrounding Content##

##Range modification under document mutation##

##参考文档##

1.	[Document Object Model Range](http://www.w3.org/TR/DOM-Level-2-Traversal-Range/ranges.html)