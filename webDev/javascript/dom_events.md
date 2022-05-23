
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