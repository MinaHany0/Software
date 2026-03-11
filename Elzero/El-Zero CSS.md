# 07 padding

div{
background-color: #DDD;

padding: 10px;
padding-top: 10px;
padding-left: 10px;
padding-bottom: 10px;
padding-right: 10px;

# 08 Margin
```
p {
    background: red;
    padding: 10px 20px 15px 25px;
    margin: 10px;
    width: 50%;
    margin-left: auto;
    margin-right: auto;
    margin: auto;
}
```
# 09 Border
```
.facts {
    border-radius: 30px;
    border-color: green blue;
    border-width: 10px;
    border-style: solid;

    /* 
    or you can write them in a combined attribute directly like in the following
    border: 5px dashed red 30px; 
    */
}
```

# 10 Outline
the outline does the same job as the border but it has many restrictions and it can't be decided for four side, instead you give one value for all side
- no need to use the outline, you just know it for the info itself.

# 11 Block vs Inline vs Inline block

Blocks:
- respects padding, margin, width and height
- takes full width by default
- adds a line break by default

Inline:
- takes only available width 
- doesn't respect paddings, margins, width or height.
- doesn't add a line break by default

Inline block
- doesn't add a line break by default
- respects margins, padding, width and height

# 12 Element Visibility and Use Cases

there is two attributes to control visibility which are display and visibility

```
.div{
display: none;
visibility: hidden;
}
```
- display control whether the whole block is displayed or not like literally the page changes
	- it can be used like to open a list (expand or hide)
- visibility controls whether the text or the element is visible on the page or not, BUT the block space doesn't get hidden, only the text

# 13 Grouping multiple selectors
if you have multiple common attributes for multiple selectors and you need to change them at the same time
- just have them common attributes be written one time with the grouped selectors with the next syntax
```
.div1,
.div2,
,div3{
margin: 20px;
color: red;
background-color: #EEE;
}
```
and so if you want to change the common attribute value, it changes for all the grouped selectors at the same time.

# 14 Nesting
you need to put the multiple selectors inside each other in a logical order
ex:

```
div .class p {
color: red;
}
```

# 15 Dimensions
attributes:
- width
- height
- min-width
- max-width
- min-height
- max-height

- to have the blocks be arranged in a side by side view we have few options
	1. giving them "inline-block" attribute , <span style="color:rgb(255, 192, 0)">but this is not best practise</span> 
	2. giving them "<span style="color:rgb(255, 192, 0)">width: fit-content</span>" and <span style="color:rgb(255, 192, 0)">this is the new best way</span> 

# 16 Overflow
there is an attribute called overflow that is used to control the ooverflow in the x and y directions
its values are 
1. hidden
2. scroll
3. visible
4. auto

# 17 text color and shadow
- text-shadow: 1px 1px 1px red;
- background-color: red;
- color:blue;

# 18 Text Alignment 
- text-align: center;
- direction: ltr (left to right);
- direction rtl;

# 19 text decoration
- text-decoration: underline;
- text-transform: capitalize;

# 20 text spacing
- letter-spacing: 1px;
- text-indent: 100px;
- line-height: 160%;
- word spacing: 5px;
- white-space: normal; // nowrap;

# 22 Inheritance

- properties can be inherited.
- if you specify an attribute in a child member, then the child attribute overrides the one that was inherited from the selector parent which makes perfect sense.
- there is value for the attributes called <span style="color:rgb(255, 192, 0)">"inherit"</span> which specifies the child selector to inherit the value from the parent selector incase this property doesn't inherit and usually has a default value from the css or the browser.

# 23 Fonts

sans serif: without the extra edges
serif: with edges

# 24 Font size and CSS units
default font size = 16 px
1 em = time :) 

# 25 Font Variant , Text Transform
# Mouse Cursor
you can change cursor look based on the item the cursor is looking at
ex: 
```
<div> 
	cursor: clickable;
	cursor: pointer;
</div>
```
- many looks for the pointer is there and it is used to enhance the user interface.

# 27 float and clear

the float property is used to have the elements hang freely in the web page
- instead of giving the div an "inline block" property and having to adjust them manually
- just give them the float property to give them the inline look
- you will need to use the overflow property with the float on the parent div, otherwise the border and margins all will get distorted. so you need to organize the floating stuff in the frame or in the "border" so you use "overflow: hidden" just to have the border and margin fully wrap the floating elements

the clear property is used to stop the effect of the float until a certain point
- for example you put a div with a class clear at a certain point and give it a clear property in the CSS sheet
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Test number 1</title>
    <link rel="stylesheet" href="./test.css">
</head>
<body>
    <div class="parent">
        <div> first button</div>
        <div> second button</div>
        <div> third button</div>
        <p  class="clear"></p>
    </div>

    <p>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Sed harum eos alias sapiente ratione, obcaecati impedit officiis temporibus, cum quo quod exercitationem iste quas reprehenderit deleniti! Dignissimos modi laudantium neque!</p>
</body>
</html>```

```css
.parent{
    background-color: #EEE;
    margin: 20px;
    padding: 20px;
    border:red 5px solid;
    overflow: hidden;
}

.parent div{
    background-color: yellow;
    font-weight: bold;
    padding: 10px;
    margin:10px;
    font-family: 'Courier New', Courier, monospace;
    float: left;
    width: 30.33%;
}
 
.clear{
    clear: left;
}
```


# 28 Mastering CSS calculation
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>width-calculation</title>
    <link rel="stylesheet" href="test2.css">
</head>
<body>
    <div class="parent">

        <div> product one</div>
        <div> product two</div>
        <div> product three</div>
        <div> product four</div>
        <p class="clear"></p>
    </div>
</body>
</html>
```

```css
body{
    margin: 0;
}


.parent{
    background-color: #EEE;

}

.parent div{
    padding: 20px 0px;
    background-color: aqua;
    text-align: center;
    float: left;
    margin-left: 10px;
    width: calc((100% - 5*10px)/4);
    
}

.clear{
    clear: both;
}
```

# 29 Opacity
used when a pop up happens for example to dim the rest of the page and have the pop up highlighted
```css
opacity:0.5;
```

# 30 Position
position property has 3 most used values:
- relative
- absolute
- fixed
## Relative
you can use the 4 direction properties (top bottom left right) with the relative to move the object relative to its normal position and it won't respect anything in the web page but itself
## Absolute
absolute just removes the element from the normal HTML sequence because it knows you will coordinate it in some fixed place in the page, so there is no need to hold some space hostage for some element that is never coming back

- Hint: 
	if you put the absolute element in a big element with a position = relative value, then it will move abosuletly relative to that parent element
## Fixed
fixed is the same as absolute where the browser doesn't spare a space in the HTML normal sequence but the difference is that the <span style="color:rgb(255, 192, 0)">element will be still even when you scoll</span> 
- this is used like in a fixed button on the page no matter where you go

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>width-calculation</title>
    <link rel="stylesheet" href="test2.css">
</head>
<body>
    <div class="big">
        <div class="l-product">this is the last product</div>
    </div>
    <div class="parent">
        <div> product one</div>
        <div> product two</div>
        <div> product three</div>
        <div> product four</div>
        <p class="clear"></p>
    </div>
</body>
</html>

```

```css
body{
    margin: 0;
}


.parent{
    background-color: #EEE;

}

.parent div{
    padding: 20px 0px;
    background-color: aqua;
    text-align: center;
    float: left;
    margin-left: 10px;
    width: calc((100% - 5*10px)/4);
    
}

.clear{
    clear: both;
}

.l-product{
    position: absolute;
    bottom: 0;
    right: 50%;
    background-color: turquoise;
    width: 200px;
    text-align: center;
    padding: 30px;
}

.big{
    height: 600px;
    background-color: yellow;
    position:relative;
    
}
```

# 31 Z index
the Z index is the number indication which object will appear above which object

# 32 List styling
it explains how to change the icon of the list and how to re-arrange a list for example to use in a navigation bar , it gives a hint of the before and after usage which will replace all of the list styling properties

# 33 Tables Styling
really beautiful to be able to style a table and give it colors and borders

# 34 Pseudo Classes
pseudo classes is a way of giving value for some cases of properties
for example if the paragraph is empty to change its color
so --> p:empty{  } --> this helps in giving conditional properties like : hover or visited links or .... etc

# 35 Pseudo Elements
what are pseudo elements ?
pseudo elements are elements that are given properties (as it is in the normal case) but they are not actually there
	- example is giving the first letter in a paragraph different styling as in books, so instead of making the first letter itself an element by putting it in an element or a span, you can use pseudo elements: --> div::first-letter {  } 
		- <span style="color:rgb(255, 192, 0)">notice that: one colon was used before for both pseudo classes and pseudo elements but later in CSS 3 , it was chosen that two colons are for pseudo elements while one is for classes</span> 
	- a harder example would be giving the first line some properties, since the first line is decided based on the viewing screen, so instead of programming the width that changes you can just use pseudo elements
# 36 Before and After Pseudo Properties
property::after{
}

and 

property::before{

}

refer to videos for further reference but I already applied and done the homework
take this assignment for example

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>assign11-4</title>
    <link rel="stylesheet" href="assign11-4.css">
</head>

<body>
    <p>This Is Very Very Long Product Title</p>
    <p>This Is Very Very Long Product Title</p>
    <p>This Is Very Very Long Product Title</p>
    <p>This Is Very Very Long Product Title</p>
    <p>This Is Very Very Long Product Title</p>
    <p>This Is Very Very Long Product Title</p>
</body>

</html>
```

```css
p::before {
    content: counter(number);
    width: 20px;
    height: 20px;
    color: white;
    background-color: #f44336;
    position: absolute;
    padding: 20px;
    left: -10px;
    top: 0;
    font-weight: 500;
    margin-top: 0;
}

p {
    counter-increment: number;
    width: 400px;
    background-color: #EEE;
    padding: 20px;
    margin: 20px auto;
    position: relative;
    font: 20px bold;
    text-align: center;
}

p::after{
    content: "";
    width: 5px;
    height: 100%;
    background-color: #f44336;
    position: absolute;
    top: 0px;
    right: 0px;
}
```

# 38 Vendor prefixes

-webkit -> for chrome, new opera, ...
-moz -> for mozilla
-ms -> for edge or IE

this is used for any beta feature until it is fully supported in the browser

# 39 Border radius

# 40 Box Shadow and examples

# 41 Box model and Box sizing
default box model is the content box
the other type is the border box

# 42 Transitions

# 43 Important flag
is used when you need to override over the same property when the html has multiple css files by different users but you have no access to modify the first file or to modify the inline styling in the generated html file itself


# 44 Margin Collapse
the vertical margin collapses and combines but horizontal margin do NOT

# 45 CSS Variables and training
we have global and local variables
you can set them by writing
```
--mainColor : blue;
```
and then use them in the syntax of var(variableName, fall back value)
where the fall back value is the value to use if the variable was not found

```
background-color: va(--mainColor, red);
```

# 46 Flex box parent (direction, wrap, flow)
instead of doing float and managing each element
- you can put in parent div the property
	- display: flex
	- then use flex direction = row, row reverse, column, column reverse
	- also use flex wrap: nowrap, wrap or wrap-reverse
	- or use flex flow which has both properties of wrap and direction and put the value of row wrap directly

# 47 Flex box parent (justify content)
will bring all the elements to a side (left , right or center)
- if you want space in between elements
	- in float we need to use margin left and right for each element after calculating and assigning the width
	- using flex we can just use the value: "space between" if you need spaces only in between elements like spaces with distribution ( 0 on side , 1 , 1, 1, 1, 1, 0 on side)
	- or use the value "space around" if you want spaces in between and also around the elements like (1, 2, 2, 2, 2, 1)
	- or you can use the value "space evenly" for equal space distribution between the elements (1, 1, 1, 1, 1, 1, 1)

# 48 Flex box parent (align items)
- we saw how justify content is used for the horizontal alignments
- now the vertical alignment is done using the align items property in the flex
	- default value is stretch ----- <span style="color:rgb(255, 192, 0)">notice that align items can make text in the center of a box or can make a div be stretched in another div or be just at the start with the default height</span>
	- other values are (flex-start, center, flex-end)

# 49 Flex box parent (align-content)
align content is similar to align items but it works on the content as a whole
- for example if you have two rows it will treat the two rows as one item not two separate rows
- which can be useful in some cases

# 50 Flex box child (flex-grow, flex-shrink, order)

- flex-grow is used to give priority to which element to grow when the width of the parent element is bigger than the sum of the child elements
- flex shrink is the priority of which element to shrink to fit all the elements if the parent element is smaller than the sum of children width
- order property is used to shuffle the elements and replace them but remember that if you put element 6 in place of element one-> then you need to tell the browser where to put element 1 and so on for the rest of the elements
# 51 Flex box child (flex basis)
- flex basis is the replacement for the width or height property inside the flex box
- because of you use width and then change the flex direction to column instead of row, the item height will not change based on the decided width
- <span style="color:rgb(255, 192, 0)">but with flex basis you can perfectly transpose the row to a height with the preferred dimension in both width or height</span> 

- you can use the shorthand property flex for short of the 3 properties with the following syntax
	- flex = (flex-grow , flex-shrink, flex-basis) with the default values  = (0 , 1 , auto)
- you can use the property <span style="color:rgb(255, 192, 0)">display: inline flex</span>  to make the flex itself inline with another element that has inline property value beside it on the same line 

# 52 Flex box child (self align)
align self property takes value : flex-start, flex-end, .... which center the element or moves it to start or end

# 53 Flexbox Frog exercise

# 54 Filters
# 55 Gradient colors
# 56 Pointer Event and caret colors
there is this property where you can cancel the effect done by pointer like hovering effects or following a link when you click on it which is an event cancelled when you make the pointer event property none

# 57 Grid Parent .. Template Column

# 58 Grid Parent .. Template Row .. gap

to make template rows or columns you need
- property display: grid;
- property grid-template-columns: where you can give values
	- 100px 200px 400px
	- 100px 25%  1fr auto
	- repeat (2, auto) 200px 400px
- <span style="color:rgb(255, 192, 0)">fr (fraction) is as greedy as possible while the auto takes as much as needed for the element and taking other available space is not used by other elements</span> 
- the same applies for grid-template-rows

to make gaps between columsnor rows you need the property (column-gap or row-gap) or you can use the property gap which takes two values for columns and rows

# 59 Grid Parent .. Justify-content and Align-content

# 60 Grid Parent .. Complete layout with template areas
ex: 

``` css

page{
	display:grid;
	grid-template-columns:repeat(10,1fr);
	grid-template-rows: 50px auto 50px;
	grid-template-areas:
		"logo logo logo navi navi navi navi navi navi navi navi"
		"cont cont cont cont cont cont cont cont cont side side"
		"foot foot foot foot foot foot foot foot foot foot foot"
}
h2{
	grid-area:logo;
}
nav{
	grid-area:navi;
}
footer{
	grid-area:foot;
}
content{
	grid-area:cont;
}
```

this will make the normal layout known in pages that will look like this ![[El-Zero CSS-20250413203426383.webp]]

# 61 62 63 Grid stuff
![[El-Zero CSS-20250413214319483.webp]]

# 64 Transform - scale

``` css
transform: scaleX(2);
transform: scale(2,-1);
```
this can be used along with the transition properly during the hovering pseudo state to give the illusion of rotating or enlargement onhovering
![[El-Zero CSS-20250420191620583.webp]]
