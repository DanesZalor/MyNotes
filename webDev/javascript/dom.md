# Document Object Model
Represents the document as a tree structure. HTML elements become interrelated **nodes** in the tree.
Nodes have **child** nodes. Nodes on the same tree level are called **siblings**
![DOM](.imgs/domdiagram.png)
> `<html>` has two children; `<head>` and `<body>`

```javascript
document.body.innerHTML = "<h1> yo </h1>";
```
outputs:<br>
![sampleoutput](.imgs/sampleinnerhtml.png)


## Selecting elements
All HTML elements are **objects**. The **document** object has methods that allow you to select the desired HTML element. Example:
```html
<html>
    <head>
        <title>Titlepage</title>  
    </head>
    <body>
        <h1 id="header1"> hello </h1>
        <div id="div1">
            <p class="prg">This is paragraph1</p>
            <p class="prg">This is paragraph2</p>
        </div>
    </body>
</html>
```

```javascript
document.getElementById("div1");
```
> outputs: `<div id="div1">`

```javascript
document.getElementsByClassName("prg");
```
> outputs: `HTMLCollection { 0: p.prg, 1: p.prg, length: 2 }`

```javascript
document.getElementsByTagName("p");
```
> outputs: `HTMLCollection { 0: p.prg, 1: p.prg, length: 2 }`
> `HTMLCollection` can be used **like an array**

### DOM Element Properties

|Property|description|<sub><sup>Using the same example above</sup></sub>|
|-|-|-|
|`innerHTML`|<sub><sup>gets the absolute HTML text inside the element including line breaks and tags|`document.getElementById("div1").innerHTML;`<br> <sub>`"\n            <p class=\"prg\">This is paragraph1</p>\n            <p class=\"prg\">This is paragraph2</p>\n   `</sub>|
|`innerText`|<sub><sup>gets the inner text trimmed|`document.getElementById("div1").innerText;`<br><sub>`"This is paragraph1\n\nThis is paragraph2"`</sub>|
|`children`|<sub><sup>returns an array of the child nodes|`document.getElementById("div1").children`<br><sub>`HTMLCollection { 0: p.prg, 1: p.prg, length: 2 }`</sub>|
|`parentNode`||`document.getElementById("div1").parentNode`<br><sub>`<body>`|
|`firstElementChild`||`document.getElementById("div1").firstElementChild.innerText`<br><sub>`"This is paragraph1"`|
|`lastElementChild`||`document.getElementById("div1").lastElementChild.innerText`<br><sub>`"This is paragraph2"`|
|`previousElementSibling`|||
|`nextElementSibling`|||

> I dunno my learning resource showed different information. must be outdated.
> <br>You can always check using your browser console though

## Changing Element Attributes
Say we have this project:<br>
![img](.imgs/sampleelementchange.png)

we can change `#img1.src` by doing:

```javascript
document.getElementById("img1").src = "asset/img2.png" 
```

You can even change style properties:
```javascript
document.getElementById("div1").style.backgroundColor = "#dcdddf";
```

## Adding & Removing Elements

```javascript
element.cloneNode();
```
to clone an element. if you append an element that is in the tree, it will move and fuck up the tree.

```javascript
document.createElement(element);
```
 creates a new element w the tag name : *element* parameter

 ```javascript
 var elem = document.createElement("div");
 elem.id = "div3";
 elem.innerText = "i hate sex";

document.appendChild(elem);
```
adds the element
```html
<div id="div3">i hate sex</div>
```

to remove a child:
```javascript
element.removeChild(elem);
```

to replace a parent's child with a newOne:
```javascript
parent.replaceChild(newOne, child);
```

### Animations
![animationcss](.imgs/animationcss.png)

> `setInterval(handler, ms, args?)` will call `handler` with parameters `args` every `ms` milliseconds.<br>
> `clearInterval(obj)` will stop the shit idk what object type it returns because JAVASCRIPT is so goddamn confusing <3


## Events
|event|description|
|-|-|
|`onclick`|when element is clicked|
|`onload`|when element is loaded|
|`onunload`|when a page has unloaded (for `<body>`)|
|`onchange`|occurs when the content of a form element, selection or the checked state have changed.<br> for `<input>, <keygen>, <select>, <textarea>`|
|`onmouseover`|when the pointer is **moved onto** an element or one of its children|
|`onmouseout`|when the pointer is **moved out of** an element or one of its children|
|`onmousedown`|occurs when the user **pressed** a mouse button over an element|
|`onmouseup`|occurs when the user **released** a mouse button over an element|
|`onblur`|occurs when an element **loses focus**|
|`onfocus`|occurs when an element **gets focus**|

corresponding events can be added to HTML elements as attributes like: <br>
```html
<p onclick="someFunc()">Some text</p>
<script>
function someFunc(){
    alert("death");
}
</script>
```

in javascript, you can set these event handlers by assigning a function to them:
```javascript
var x = document.getElementById("someid");
x.onclick = function(){
    // some code to execute
}

// alternatively

function someFunc(){
    // some code
}

x.onclick = someFunc;
```

### Event Listener
the `addEventListener()` method connects an event handler to an element without overwriting existing event handlers. You can add *many* event handlers to one element, or many event handlers to the same type to one element. like two "click" events.

```javascript
element.addEventListener(event, func, useCapture);
```
**`event`** param is a string of which event. If you want to handle an `onclick` event, you use `"click"` arguement.<br>
**`func`** is the function we want to call when the event occurs.<br>
**`useCapture`** is a boolean specifying whether to use event **bubbling** or event **capturing**. but this parameter is optional.

```javascript
element.removeEventListener(event, func, useCapture);
```
use this method to remove listeners. the parameters are the same.

Example:

```html
<html>
	<head>
		<title>Page Title</title>
	</head>
	<body>
		<button id="btn1">Click Me please</button>
		<button id="btn2">Click Me to shut button 1 up</button>
		<script src="index.js"></script>
	</body>
</html>
```

```javascript
var btn1 = document.getElementById("btn1");
var btn2 = document.getElementById("btn2");

function btn1_click() {
    alert("you clicked me.");
}

btn1.addEventListener("click", btn1_click);

btn2.addEventListener("click", function () {
    alert("now i will remote btn1 event listener");
    btn1.removeEventListener("click", btn1_click)
});
```