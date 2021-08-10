## HTML Hyper Text Markup Language


comment: `<!-- This is a comment -->`

`<!DOCTYPE html>`: to use the full standards mode

<meta name="description" content="dwedwedwed" />


### Tags

`html`
`body`
`head`

 - `p`
 - `h1-h6`
 - `bold`
 - `strong`
 - `i`
 - `em`
 - `sup`
 - `sub`
 - `blockquote`
 - `div`
 - `span`: similar to div but works for a single element
 
 
`ul`
`ol`
`li`

`a`
 
 - href="#name" 
 
 - `iframe`
   - `src`

attributes:

 - title
 - alt

#### Tables

`table`
`th`
`tr`
`td`

    <table>
      <tr>
        <th>header1</th>
        <th>header2</th>
        <th>header3</th>
      </tr>
      <tr>
        <td>data1</td>
        <td>data2</td>
        <td>data3</td>
      </tr>
    </table>

#### form

 - `form`
 - `input`
   - `type`
     - `text` 
     - `radio`: use the same `name` attribute to tie all together. Radio is used to select one of the items
     - `submit`: `value` is the text of the button
     - `checkbox`
     - `number`: `min` `max`
     - `date`
     - `tel`
     - `email`
   - `size`: number of chars
 - `label `
 - `textarea`
   - `rows` `cols`: num of chars
 - `fieldset`
 - `legend`

sample: 

    <label for="name"></label>
    <input type="text" id="name">

#### drop-down list

    <select>
      <option value="michigan">michigan</option>
      <option value="michigan">utah</option>
    </select>

#### empty element

element that cannot have any child nodes

 - `br`: line break
 - `img`
   - `src`
   - `width`
   - `height`

### HTML entity

 - `&nbsp;` no breakable space
 - `&lt`: <
 - `&gt`: >
 - `&amp;`: &


## CSS Cascading Style Sheets

 - internal style sheet
   - put inside the `style`
 - external style sheet
   - `<link rel="stylesheet" type="text/css" href="mystyle.css">`

 - inline
   - `<p style="color:black;font-size:25px;">This is inline style</p>`

examples: 

    h1 {
        background-color: purple;
        border-bottom: 1px solid black;
        border: 1px solid black;         // add a box
        text-align: center/left/right;
    }
    
    p {
        color: red;
        font-size: 25px;
        font-family: Helvetica;
        font-style: italic/oblique;
        text-decoration: underline/line-through/overline;
        font-weight: lighter/normal/bold/bolder;
        line-height: 1.5em;
        background-image: url(clouds.gif);
        width: 100px; (the width of the content)
    }

    selector {
        attribute: value;
    }

opacity: 0.5

#### gradient

 - `background: linear-gradient(blue, yello)`
 - `background: linear-gradient(to right, blue, yello)`
 - `background: linear-gradient(to top right, blue, yello)`
 - `background: linear-gradient(30deg, blue, yello)`
 - `background: linear-gradient(blue, yello 20%)`
 - `background: linear-gradient(blue 50%, yello 50%)`

 
 
#### font size
 - px
 - %
 - em
 - keywords: small, medium, large...


#### Colors

 - 16 primary colors
 - rgb: `rgb(n1, n2, n3)`
 - Hex: `#ffcde5`

#### selectors

 - type selector: `body` applies to all body tags
 - class selector: `.className` class="className"
 - ID selector: `#elementId` id="elementId". Select an individual element

Multiple selectors

 - combine selectors: use ,
 - Descendent selector: select element under another element: use space
 - child selector: use > : div>p
 - nth child selector
   - `p:nth-child(even)`
   - `p:nth-child(odd)`
   - `p:nth-child(3)`
   - `p:nth-child(3n)`
   - `p:nth-child(3n + 4)`
 - slibling selector: h1+p. All sibling: h1~p
 - wildcard selector: *
 - attribute selector: 
   - `p[lang]`
   - `p[lang="fr"]`
   - `p[lang^="fr"]` begins with
   - `p[lang$="fr"]` ends with
   - `p[lang*="fr"]` contains
 - not selector
   - `:not(p)`
   - needs to have a `p` selector to make it work
 - first selector
   - `p::first-letter`
   - `p:first-line`

#### CSS inheritance and overriding

#### Box model

 - Margin
   - `margin-left`
   - `margin-right`
   - `margin-top`
   - `margin-bottom`
   - can combine into one
 - Border
   - `border-color`
   - `border-width`: thin, medium, thick or use px
   - `border-style`: solid, dashed, dotted, double, groove, ridge...
   - can combine into one 
   - `border-radius`: 10px;
     - `border-bottom-left-radius`
     - ...
   - `border-bottom-style`
 - Padding
   - padding-left
   - ...
   - can combine all four into one: top right bottom left
 - Content

Background-color applies only to padding and content

CSS 

    p {
      padding: 20px;
      border-color: black;
      border-width: 2px;
      border-style: solid;
    }
    
    img {
      display: block;
      margin-left: auto;
      margin-right: auto; // split the available margin evenly
    }

#### pseudo classes

    a:link {
      color: blue;
    }
    
    a:visited {
      color: #ffffff
    }
    
    a:hover {
      color: #ffffff
    }

#### block elements and inline element

inline element: margin of most elements apply only to the sides, not up and bottom, except img

block element will take the larger margin of the two neighbors, but inline elements will add them up 

`Span` is inline


img {
  display: block/inline/inline-block;
}

#### float a element

not in the flow

when you float an element, you are **interrupting** the flow

    float: left/right;

When you float an element, you must specify the width

#### absolute positioned element

relative to the first non-static element

**completely removed** from the element flow

    position: absolute;
    top: 75px;
    right: 50px;

#### fixed positioned element:

    position: fixed;

#### overflow

    overflow: scroll/hidden;

#### cursor:

    a:hover {
        cursor: crosshair/help/none/move;
        cursor: url("mail.ico"), default;
    }

#### relative position

determined by the nearest static element

static position: the default positioning (the flow)

#### list

    list-style-type: none;

#### center a text vertically:

line-height matches the height;

vertical-align?

#### tables

    .table {
      display: table;
    }
    
    .row {
      display: table-row;
    }
    
    .cell {
      display: table-cell
    }

style.visibility = "hiddle"

### CSS Layouts

 - fluid
 - fixed


## Javascript

 - Dynamic typed: variables don't have types. Values have types.
 - single quote and double quotes mean the same thing
 - script tag: `<script type="text/javascript" src="myScript.js">`
 - inline: inside `script` tag
 - The browser has a js engine that could execute js code
 - === vs ==
 - pass by value or reference?

#### Query Selector

element.querySelector() or element.querySelectorAll();

`[id^='someId']` will match all ids starting with someId.

`[id$='someId']` will match all ids ending with someId.

`[id*='someId']` will match all ids containing someId.



#### Variables:

delare: let, var, const, none

 - let: block scope
 - var: inside function
 - none: global

primitive types: string, number, boolean, undefined, null

reference types: Object Array Function


let vs var:


    let x;
    
    let x = 5;
    
    y = "hello";

#### Arrays

array is an object

    let colors = [];   // Array literal
    let colors = ['red', 'blue'];
    colors[0] == 'red'
    
    colors[2] = 'green'
    colors.length == 3;

#### Functions

    function myFunctioname(param1, param2) {
    
    }

Function literal syntax
 
    let myFunctioName = function(param1, param2) {
    
    }
    
#### Objects

    let x = {};  // object literal
    
    x.someField = 4; // dot notation
    x['someField'];  // Bracket notation
    
    x.aMethod = function() {
        console.log("hello world");
    }
    x.aMethod();
    
    // Object literals
    x = {a: 4, b: "hello", "2": "two"}
    
    x.a == x['a']
    x.b == "hello"
    x['2'] == "two"
    x.2  // Illegal
    
    delete x.a

#### DOM: Document Object Model

document: refers to the page

    document.getElementsByTagName( tagName ) // array of nodes
    document.getElementById( someId )        // single node
    document.getElementsByClassName( someClass ) // list of nodes
    
    // takes a string that looks like a CSS selector
    // when given a node, returns matching nodes of its children
    document.querySelector();  // returns the first match
    document.querySelectorAll();
    
    // modifying nodes
    element.style.backgroud = "rgb(255, 0, 0)";
    element.innerHTML = 'text in the node';
    document.createElement(tagName);
    element.appendChild(element);
    
    // includes elments, text, and comments
    element.childNodes;
    
    // child elements
    element.children
    element.firstElementChild;
    element.lastElementChild;
    
    element.parentNode;
    element.parentElement;
    
    element.nextElementSibling;
    element.previousElementSibling;
    
    document.createTextNode("some text");
    element.remove();                           
    element.parentNode.removeChild(element);
    
    let attribute = element.createAttribute("src");
    attribute.value = "dewd.jpg";
    element.setAttributeNode(attribute);

#### Form validation

`<form action="page.html" method="post" onSubmit="return validate();">`

validate() should return a true or false

inputBox.focus();

confirm("text"): returns a boolean

Redirect to a new page: window.location = "newpage.html";











