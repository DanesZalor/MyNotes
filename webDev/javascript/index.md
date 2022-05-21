# JavaScript

Say we have this php file `index.php`
```php
<html>
    <head>
        <title>Titlepage</title>  
    </head>
    <body>
        <script src="index.js"></script> 
        <h1> hello </h1>
    </body>
</html>
```

and js file `index.js`
```javascript
alert("Hello mfs");
```

What happens is, when you load the php file in the browser, it executes it line by line. Meaning that `<script src="index.js"></script>` will run, and execute everything in the script before it proceeds to display the `<h1> hello </h1>`

## Objects
JavaScript variables are containers for data values. **Objects** are variables too, but they can contain many values.

Think of an object as a *php Associative array* where the elements are written as `name:value` pairs.

```javascript
var person = {
    name: "bobby",
    age: 16,
    isDead: true,
};

console.log(person.name + " is " + person.age + " years old");
console.log(person['name'] + " is " + person['age'] + " years old");
```
both logs output:
```
bobby is 16 years old
```
JavaScript's built-in **length** property is used to count the number of characters in a property or string.
```javascript
person.name.length; // 5 : b,o,b,b & y
person.age.length; // undefined wtf?
```

## The object constructor
This is creating an object using the **object literal** syntax.
```javascript
var person = {
    name: "bobby", age: 16,
    isDead: true,
};
```

This allows you to create only a single object. Sometimes, we need to set an **object type** that can be used to create a number of objects of a single type.

We can use an object **constructor function**.
```javascript
function person(name, age) {
    this.name = name;
    this.age = age;
}

var p1 = new person("bob",23);
```

### adding methods
**methods** are functions stored as object properties.
```javascript
function person(name, age) {
    this.name = name;
    this.age = age;
    this.greet = function () {
        console.log(
            "Hello my name is " + this.name + " and I'm "
            + this.age + " years old.");
    }
}

var p1 = new person("bob", 5);
p1.greet();
// outputs
// Hello my name is bobby and I'm 12 years old.
```

Since methods are properties, you can reference methods outisde and assign them to an obejct:

```javascript
function person(name, age) {
    this.name = name;
    this.age = age;
    this.greet = printGreeting;
}

function printGreeting() {
    console.log(
        "Hello my name is " + this.name + " and I'm "
        + this.age + " years old.");
}
```

## Arrays
```javascript
var arr = new Array("One","Two","Three");
arr[0]; // One
arr[1]; //Two
arr[3]; //Undefined
```

Another way to create arrays
```javascript
var arr = new Array(3); // creates an empty array with length of 3
arr[0] = "One";
```

#### Array Literal
```javascript
var arr = ["One", "Two", "Three"];
```

#### Array Properties & Methods
```javascript
var arr = ["One", "Two", "Three"];
arr.length;  // returns num of elements

var arr2 = ["Four", "Five", "Six"];
arr2 = arr.concat(arr2);
// combines the two arrays
```

#### Associative Array
JavaScript **does not** support associative arrays but you can still use the named syntax like this which will produce an object: 
```javascript
var person = [];
person["name"] = "john";

console.log(person["name"]); // john
```

## Math Object

Math Object is a built in JavaScript class for mathematical tasks. It includes several properties and methods.

|Math||
|-|-|
|<sub>Property</sub>||
|`Math.E`|Euler's constant|
|`Math.LN2`|Natural log of the value 2|
|`Math.LN10`|Natural log of the value 10|
|`Math.LN2E`|Base 2 log of Euler's constant|
|`Math.LN10E`|Base 10 log of Euler's constant|
|`Math.PI`|3.1415926535...|
|<sub>Method</sub>||
|`Math.abs(x)`|returns absolute value of x|
|`Math.acos(x)`|returns arccosine of x in radians|
|`Math.asin(x)`|returns arcsine of x in radians|
|`Math.atan(x)`|returns arctangent of x in radians|
|`Math.atan2(y,x)`|returns arctangent of x as a numeric value between `-PI/2` and `PI/2` in radians|
|`Math.ciel(x)`|returns x rounded upwards to the nearest integer|
|`Math.cos(x)`|returns cosine of x in radians|
|`Math.exp(x)`|returns $E^{x}$|
|`Math.floor(x)`|returns x rounded downwards to the nearest integer|
|`Math.log(x)`|returns the natural logarithm (base E) of x|
|`Math.max(x,y,z,..n)`|returns largest|
|`Math.min(x,y,z,..n)`|returns smallest|
|`Math.pow(x,y)`|returns $x^y$|
|`Math.random()`|returns a random number between 0 and 1|
|`Math.round(x)`|rounds x to the nearest integer|
|`Math.sin(x)`|returns the sine of x in radians|
|`Math.sqrt(x)`|returns $\sqrt{x}$|
|`Math.tan(x)`|returns the tangent of x in radians|

## Date

```javascript
var d = new Date(); // current date-time

// other ways to initialize date
new Date(dateString);
new Date(milliseconds);
new Date(year, month, day, hours, minutes, seconds, milliseconds);
```

<br>

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
Using the same example above;
```javascript
document.getElementById("div1").innerHTML;
```
> `"\n            <p class=\"prg\">This is paragraph1</p>\n            <p class=\"prg\">This is paragraph2</p>\n   `

```javascript
document.getElementById("div1").innerText;
```
> `"This is paragraph1\n\nThis is paragraph2"`