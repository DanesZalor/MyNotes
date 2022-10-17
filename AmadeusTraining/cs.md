# C# getting started

the new knowledge i acquire from the tutorial about C#

Instead of traditional "functions", C# has static methods.

Besides signed and unsigned data types, there's also **native** types such as **nint** and **nuint** which depends on the platform and they are only useful for very low programming.

for decimal types, besides float and double, there's also **decimal** which is 128 bits (much more precise)

**Type Inference** - using **var** keyword when assigning a variable so the data type is automatically assigned based on what ever value or data is assigned. It is optional and it doesn't affect the *type-safeness* of your code.

```C#
var tempC = 1.2f;
// tempC becomes a float since 1.2f is a float

string x = tempC;
// compiler error since the compiler knows tempC is a float
```

### Referencing Libraries

Normally when we use other people's code, we just copy the source code and include it into our project. But it's better to import the compiled library instead.

C# projects produce an **assembly** which is a file or sometimes a small bunch of files. In order to use a library, instead of importing the source code, we can just import the compiled library or a **DLL file** as one of the dependencies

### Alias importing
```C#
using Alias = Namespace.Class; 
```
same as `import as` in javascript


### Ternary Statements
```C#
boolean ? value1 : value2
```

### Switch statement expression
```C#
var id = param switch{
    "paramvalue1" => 1,
    "paramvalue2" => 2,
    "paramvalue3" => 3,
    _ => 0, // default
}
```

**when** keyword for more complex match selection
```C#
int discountID = 12;
switch (discountID)
{
    case int id when id < 10:
        Console.WriteLine("<10");
        break;
    case int id when id >= 10 && id < 20:
        Console.WriteLine("10-20");
        break;
    default:
        Console.WriteLine(">20");
        break;
}
```

**Type matching**
```C#
Shape myShape = new Rectangle() {width = 20};
switch(myShape){
    case Square s when shape.width < 10:
        // some code
        break;
    case Rectangle r when shape.width > 10:
        // some code
        break;
    default:
}
```