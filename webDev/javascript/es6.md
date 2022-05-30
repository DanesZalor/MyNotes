# ECMAScript
**ECMAScript** (ES) is a scripting language specification created to standardize JavaScript.

ES6 and later adds significant new syntax for writing complex applications, including classes and moodules, iterators and for/of loops, generators, arrow functions, binary data, typed arrays, collections (maps, sets and weak maps), promises, number and math enhancements, reflection and proxies.

ES6 is a superset of JavaScript (ES5). The reason that ES6 became so popular is that it introduced new conventions and OOP concepts.

## Variables
in ES6, we have three ways of declaring variables:
```javascript
var a = 10;
const b = 'hello';
let c = true;
```

The type of declaration used depends on the necessary **scope**.

### var <sub><sup>&</sup></sub> let

**var** defines a variable globally, or locally to an entire function regardless of block scope.

**let** allows you to declare variables that are limited in scope to the block, statement, or expressions they are used in.

Example:
```javascript
if(true){
    let name = 'jack';
}
console.log(name); //error
```

to demonstrate the difference:
```javascript
function varTest(){
    var x = 1;
    if(true){
        var x = 2; // same var
        console.log(x); // 2
    }
    console.log(x); // 2
}

function letTest(){
    let x = 1;
    if(true){
        let x = 2;
        console.log(x); // 2
    }
    console.log(x); // 1
}
```

You can use **let** scope in loops:
```javascript
for(let i = 0; i<3; i++){
    console.log(i);
}
```
> the `i` variable is only accessible within the scope of the for loop, where it is only needed.

### const
**const** variables have the same scope as **let** variables except that const variables are **immutable** - they are not allowed to be reassigned.
```javascript
const a = 'hello';
a = 'Bye'; // generates an exception
```

> note that ES6 code will run only in browsers that support it. 

## Template Literals
are a way to output variables in the string. Before ES6, we had to break the string like:
```javascript
let name = 'David';
console.log('Welcome ' + name + '!');
```

You can use string templates in ES6 like:
```javascript
let name= 'David';
console.log(`Welcome ${name}!`);
```

> NOTE that template literals are enclosed by the **backtick** (`) character.

It can even handle expressions.

```javascript
let a = 8;
let b = 10;
console.log(`The sum of ${x} and ${y} is ${x+y}`);
```

> To escape a backtick in a template literal, put a backslash before it.

## Loops in ES6
in JS, we commonly use **for** loop to iterate over values in a list
```javascript
let arr = [1,2,3];
for (let k = 0; k < arr.length; k++){
    console.log(arr[k]);
}
```

The **for...in** loop is intended for iterating over **enumerable** keys of an object like:
```javascript
let obj = {"name":"bob", "age":10};
for(let v in obj){
    console.log(v);
}
// outputs the keys

for (let v in obj){
  console.log(obj[v]);
}
// outputs the values
```

The **for...of** loop iterates over **iterable** objects.
```javascript
let list = ["bob", "bobba", "tea"];
for(let val of list){
    console.log(val);
}
```
> output prints the elements in the list

Remember that **strings are iterable**
```javascript
for(let ch of "Hello"){
    console.log(ch);
}
``` 

## Functions in ES6

prior to ES6, we defined functions like this:
```javascript
function add(x,y){
    var sum = x + y;
    console.log(sum);
}
```

ES6 introduces a new syntax for writing functions.
```javascript
const add = (x, y) => {
    let sum = x + y;
    console.log(sum);
}
```

The new syntax is useful for when you just need a simple function with one arguement. no longer needing to type **function** and **return**. For example:
```javascript
const greet = x => `Welcome ${x}!`;
```
> has one arguement and returns a string

If there are no parameters:
```javascript
const prompt = () => alert("Hi");
```

The syntax is very useful for inline functions. prior to ES5, we did this:

```javascript
var arr = [1,3,5,9];
arr.forEach(function(x){
    console.log(x);
});
```

Now we do this:
```javascript
var arr = [1,3,5,9];
arr.forEach(v => {
    console.log(v);
});
```

## Default parameters in ES6:

in ES6, we can put the default values right in the signature of the functions.

```javascript
function test(a, b=3, c=42){
    return a + b + c;
}

console.log(test(5)); // 50
```

and in arrow function notation:

```javascript
const test = (a, b = 3, c = 42) => {
    return a + b + c;
}

console.log(test(5)); //50
```

## ES6 Objects
JavaScript variables can be **Object** data types that contain many values called **properties**.

```javascript
let tree = {
    height: 10,
    color: 'green',
    grow(){
        this.height += 2;
    }
};
```
<sub><sup>what the fuck am i reading</sup></sub>

### Computed Property Names

Using the square bracket notation [], we can use an expression for a property name such as concatenating strings. 

#### Example 1
```javascript
let prop = 'name';
let id = '1234';
let mobile = '08923';

let user = {
    [prop]:'Jack',
    [`user_${id}`]: `${mobile}`,
};
```
results to: `{ name: "Jack", user_1234: "08923" }`

#### Example 2
```javascript
var i = 0;
var a = {
    ['foo' + ++i]: i,
    ['foo' + ++i]: i,
    ['foo' + ++i]: i
};
```

results to `{ foo1: 1, foo2: 2, foo3: 3 }`

### Object.assign()

`Object.assign()` allows us to combine multiple sources into one target to create a single new object.

```javascript
let person = {
    name: 'Jack',
    age: 18,
    sex: 'male'
};

let student = {
    name:'Bob',
    age:20,
    xp:'2'
};

let newStudent = Object.assign({}, person, student);
```

results to `{ name: "Bob", age: 20, sex: "male", xp: "2" }`

The first param is the **target object** you want to apply new properties to. Every parameter afterwards will be used as **sources** for the target. Since *student* is the 2nd parameter, it overwrites the *name* property.

This is useful because using the assignment operators `=` on object just assigns the references.

```javascript
let person = {name:'Jack', age:18};

let newPerson = person; // newPerson references person
newPerson.name = 'Bob';

console.log(person.name); //Bob
console.log(newPerson.name); //Bob
```

To avoid this (mutations), use `Object.assign()` to create a new object.
```javascript
let person = {
    name: 'Jack',
    age: 18
};

let newPerson = Object.assign({}, person);
newPerson.name = 'Bob';

console.log(person.name); //Jack
console.log(newPerson.name); //Bob
```

## Destructuring

**destructuring** assignent syntax makes it possible to unpack values from arrays, or proprties from objects into distinct variables.

### Array Destructuring

```javascript
let arr = ['1','2','3'];
let [one, two, three] = arr;

console.log(one); //1
console.log(two); //2
console.log(three); //3
```

we can also use a destructure array returned by a function

```javascript
let a = () => {
    return [1,3,2];
}

let [one, ,two] = a();
```
array destructuring syntax also simplifies assinment and swapping values:
```javascript
[c, d] = [d, c]; // swaps
```

### Object Destructuring

```javascript
let obj = {h:100, s: true};
let {h,s} = obj;

console.log(h); //100
console.log(s); //true
```

```javascript
let a, b;
({a, b} = {a: 'Hello ', b: 'World'});

console.log(a + b); // Hello World
```

> the () with ; at the end are **mandatory** only when destructring without a declaration. However, you can do it like this:

```javascript
let {a,b} = {a:'Hello ', b: 'World'};
console.log(a + b); // Hello World
```

You can also assign the object to new variable names.

```javascript
var o = {h:42, s:true};
var {h:foo, s: bar} = 0;

console.log(h); // Error
console.log(foo); // 42
```
<sub><sup>._. what the fuck am i reading seriously</sup></sub>

Finally, you can assign **default value** to variables, in case the value unpacked from the object is undefined. For example:

```javascript
var obj = {id:42, name: "Jack"};
let {id = 10, age = 20} = obj;

console.log(id); // 42
console.log(age); // 20
```

## Rest Parameters

prior to ES6, if we wanted to pass a variable number of arguements to a function, we could use the **arguement** object which is an array-like object to access the parameters passed to the function
```javascript
function containsAll(arr){
    for(let k=1; k<arguements.length; k++){
        let num = arguements[k];
        if(arr.indexOf(num) === -1)
            return false;
    }
    return true;
}

let x = [2,4,6,7];
console.log(containsAll(x, 2,4,6,7)); // true
console.log(containsAll(x, 2,5,6,7)); // false
```

> we can pass any number of arguements to the function and access it using the **arguements** object. <sub><sup>WHO THE FUCK THOUGHT THIS WAS A GOOD IDEA????</sup></sub>

ES6 provies a more readable syntax to do the same job using the **rest parameter**.

```javascript
function containsAll(arr, ...nums){
    for(let num of nums){
        if(arr.indexOf(num) === -1)
            return false;
    }
    return true;
}
```

> if there are no extra arguments, the rest parameter will simply be an empty array; but it will never be undefined.


## Spread Operator

it is common to pass the elements of an array as arguments to a function

```javascript
function myFunction(w,x,y,z){
    console.log(w + x + y + z);
}

var args = [1,2,3];
myFunction.apply(null, args.concat(4));
```

ES6 provides an easy way to do the example above with **spread operators**.

```javascript
const myFunction = (w, x, y, z){
    console.log(w + x + y + z);
};

let args = [1,2,3];
myFunction(...args, 4);
```

one good Example is:
```javascript
var dateFields = [1970,0,1];
var date = new Date(...daetFields);
console.log(date);
```
Another example:
```javascript
const vec2 = function (x, y) {
    this.x = x;
    this.y = y;
    this.toString = () => {
        return `vec2(${this.x},${this.y})`;
    }
}

var v3 = {
    ...new vec2(4,5),
    z: 10,
    toString: function() {
        return `vec3(${this.x},${this.y},${this.z})`;
    }
}

v3.toString(); // vec3(4,5,10);
```

## ES6 Classes

ES6 classes are effectively just syntactic sugar on top of Javascript standard prototype-based inheritance system. It has a shorthand that does nto require the keyword **function**.

```javascript
class Rectangle {
    constructor(height, width){
        this.height = height;
        this.width = width;
    }

    get area(){
        return this.calcArea();
    }

    calcArea(){
        return this.height * this.width;
    }

    static calcArea(height, width){
        return height * width;
    }
}

const square = new Rectangle(5,5);
console.log(square.area); // 25
console.log(Rectangle.calcArea(4,5)); // 20
```
### Inheritance
```javascript
class Animal {
    constructor(name){
        this.name = name;
    }

    speak(){
        console.log(`${this.name} makes a noise.`);
    }
}

class Dog extends Animal {
    speak(){
        super.speak;
        console.log(`${this.name} barks.`);
    }
}

let dog = new Dog('Rex');
dog.speak();
```

> use **`super`** to access the base class properties/methods.

## Map & Set 

**Map** object can be used to hold **key/value** pairs. A key or value in a map can be anything (objects and primitive values).

An **Object** is similar to **Map** but:
- the keys can be any type including functions, objects, or primitive.
- you can get the size of a Map.
- you can directly iterate over a Map.
- performance of the Map is better in scenarios involving frequent addition and removal of key/value pairs.

```javascript
let map = new Map([['k1', 'v1'], ['k2', 'v2']]);

console.log(map.size); // 2
```

|Methods||
|-|-|
|`set(key,value)`| adds a specified key/value pair to the map. If the specified key already exists, it is replaced with the new one|
|`get(key)`|gets the value corresponding to a specified key|
|`has(key)`|returns true if key exists|
|`delete(key)`|deletes the key/value pair|
|`clear()`|removes all key/value pairs|
|`keys()`|returns an iterator of keys in the map for each element|
|`values()`|returns an iterator of values in the map for each element|
|`entries()`|returns an iterator of `array[key,value]` in the map for each element|

example:
```javascript
let map = new Map();

map.set('k1', 'v1').set('k2', 'v2');

console.log(map.get('k1')); // v1
console.log(map.has('k2')); // true

for (ley kv of map.entries())
    console.log(`${kv[0]} : ${kv[1]}`);
```

> map supports different data types <br>
> 1 and "1" are two different key/values.

A **Set** object can be used to hold **unique** values (no repetitions). A value can be anything (objects and primitive).

```javascript
let set = new Set([1,2,4,2,59,4,9,1]);

set.size; // 5
```

|Methods||
|-|-|
|`add(value)`|adds a new element|
|`delete(value)`|deletes an element|
|`has(value)`|returns true if value exists|
|`clear()`|clears the set|
|`values()`|returns an iterator of the set values|

example
```javascript
let set = new Set();

set.add(5).add(9).add(59).add(9);

console.log(set.has(9)); //true

for(let v of set.values())
    console.log(v);
```
> **Set** supports different data types like **Map**<br>
> `NaN` and `undefined` can also be stored in the Set
<sub><sup>ok wtf why?</sup></sub>

## Promises

*Producing code* is code that can take some time. <br>
*Consuming code* is code that must wait for the result.<br>
A Promise is an object that links both.

```javascript
let myPromise = new Promise(function(resolve, reject){
    // "producing code" (may take some time) 

    resolve(); // when successful
    reject();  // when error
});

// "consuming code" (must wait for a fulfilled Promise)
myPromise.then(
    function(value){ /*code if successful*/},
    function(error){ /*code if error*/}
);
```

Promise object can be:
- pending
- fulfilled
- rejected

The promise supports two properties: **state** and **result**.

Wile a promise is *pending*, the result is undefined.<br>
When a promise is *fulfilled*, the result is a value.<br>
When a promise is *rejected*, the result is an error object.

#### example

```javascript
let myPromise = new Promise(function(resolve, reject){
    let x = 0;

    if(x === 0) resolve("OK");
    else reject("Error");
});

myPromise.then(
    function(value){console.log(value);},
    function(error){console.log("ERROR! " + error);}
)
```
You can use promises to handle resolve and reject. Like if you're accessing an API to retrieve some data.


```javascript
let myPromise = new Promise(
  function(resolve, reject){
    setTimeout(function(){
        resolve("fuck NATO");
    }, 3000);
});

myPromise.then(function(value){
    console.log(value);   
})
```

> prints `"fuck Nato"` after 3 seconds.

Sources
- [Promise Object](https://www.w3schools.com/js/js_promise.asp)
- [Async-await](https://www.w3schools.com/js/js_async.asp)

## Async

async and await make promises easier to write.<br>
**async** makes a function return a promise.<br>
**await** makes a function wait for a promise.<br>


>```javascript
>async function myFunc(){
>   return "Hello";
>}
>```
> is the same as:
>```javascript
>function MyFunction(){
>   return Promise.resolve("Hello");
>}
>```

Then you can use the promise like:
>```javascript
>myFunction().then(
>   function(value){ /*code if successful*/}
>   function(error){ /*code if error*/ }
>);
>```
