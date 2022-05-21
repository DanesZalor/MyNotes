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
```
outputs:
```
bobby is 16 years old
```
