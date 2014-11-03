[Visual formatting model](http://www.w3.org/TR/CSS2/visuren.html)

##CSS渲染流程



##定位机制（Positioning schemes）

1.	**Normal flow:** In CSS 2.1, normal flow includes block formatting of block-level boxes, inline formatting of inline-level boxes, and relative positioning of block-level and inline-level boxes.
2.	**Floats:** In the float model, a box is first laid out according to the normal flow, then taken out of the flow and shifted to the left or right as far as possible. Content may flow along the side of a float.
3.	**Absolute positioning:** In the absolute positioning model, a box is removed from the normal flow entirely (it has no impact on later siblings) and assigned a position with respect to a containing block.

>NOTE: 
>
>An element is called out of flow if it is **floated**, **absolutely positioned**, or is **the root element**. An element is called in-flow if it is not out-of-flow. 
>
>The flow of an element A is the set consisting of A and all in-flow elements whose nearest out-of-flow ancestor is A.
>
>NOTE:
> 
>An element is said to be positioned if its 'position' property has a value other than 'static'. 