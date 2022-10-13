# OOP

ES6 is full of syntactical sugar that ultimately gets translated to javascript because javascript is a huge mess that they tried to make it more organized and failed so bad its so bad I want to commit genocide.

## Object
the Javascript Object has properties that you can assign to literally anything.

[Resource](https://medium.com/@mandeepkaur1/object-literal-vs-constructor-in-javascript-df143296b816)

### Object literal
object literals are singletons and are made using object literal notation. You create an object and specify it's properties on the spot.
```javascript
const obj = {
    x: 10,
    y: 12,
    toString : function() {
        let str = `(${this.x},${this.y})`;
        return str;
    }
}
```

### Prototype
You have a function that's like a template for generating an object.
```javascript
const vec2 = function (x, y) {
    this.x = x;
    this.y = y;
    this.toString = () => {
        return `vec2(${x},${y})`;
    }
}

var v2 = new vec2(10,20);
v2.toString(); // returns "vec2(10,20)"
```

## Inheritance
using Constructor and object literal notation:
```javascript
const vec2 = function (x, y) {
    this.x = x;
    this.y = y;
    this.ToSTR = () => {
        return `vec2(${this.x},${this.y})`;
    }
}

var v3 = {
    ...new vec2(4,5),
    z: 10,
    ToSTR: function() {
        return `vec3(${this.x},${this.y},${this.z})`;
    }
}

v3.toString(); // vec3(4,5,10);
```

`...new vec2(4,5)` spreads vec2 properties to the object literal. Additional properties are added and if there is one with already existing name such as `toString`, it is overrided. 

```javascript
const vec3 = function (x, y, z) {
    vec2.call(this, x, y); // the super equivalent
    this.z = z;
    this.ToSTR = () => {
        return `vec3(${this.x},${this.y},${this.z})`;
    }
}

// static property
vec3.staticvar = "Estoy estatico";
```

## IDEA
Use this base class as a **Node** to make subclasses of it as components like in React:
```javascript
/**
 * 
 * @param {str} tagName name of html tag like 'div'|'p'|'amogus' 
 * @param {object} properties object with properties 
 * @returns HTMLElement with the **properties**  assigned to it
 */
const DOMNode = function (tagName, properties = {}) {
    let dO = document.createElement(tagName, { prototype: HTMLElement.prototype });
    Object.assign(dO, properties);
    return dO;
}

export { DOMNode };
```

then you can use it like this:
```javascript
import { DOMNode } from "./jsClass/DOMNode.js";

var dn = new DOMNode('p', { innerHTML: 'sex', onclick: () => { alert('DO NOT CLICK'); } });
document.getElementById('root').appendChild(dn);
```

## Function override
say we wanna override a function but use it's base implementation like:
```C#
virtual void func(){
    Console.Write("base func");
}

override void func(){
    base.func();
    Console.Write("new func");
}
```

We do this:
```javascript
let baseFunc = THIS.func;
THIS.func = function () {
    baseFunc();
    // additional code
    console.log("call new func with baseFunc");
}
```