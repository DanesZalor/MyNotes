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

---
## Ternary Statements
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

---

## C# Types
**Predefined types** are built-in while **user-defined types** are coded by users.

**Value data types** include basic data types such as **int** and **boolean** but also user defined types such as **enum** and **struct**. *Stored on the stack*

**Reference Data types** include **String**, **Array**, **Class** and **Interface**. *Stored on the heap*

double, float, int, byte, etc are all **ValueType** while String, Array, Exception and File are all **Object**.<br>BUT ValueType is actually an Object

```C#
int x = int.MaxValue;
// notice how int is like a class that has a static variable called MaxValue

char c = 'a';
char c2 = char.ToUpper(c);
// notice how char has static methods as well
```

### Working with Dates

```C#
DateTime someDate = new DateTime(2021, 03, 28);
var today = DateTime.Today;
var twoDaysLater = someDate.AddDays(2);
DayOfWeek day = someDate.DayOfWeek;
```

### Conversions

```C#
/** Implicit cast
    data won't get lost
*/
int a = 1234;
long l = a; // same

/** Explicit cast
    data could get losts
*/
double d = 3.14;
int a = (int)d; // 3

/** Using a helper*/
double d = 12345.0;
int a = (int)Convert.ChangeType(d, typeof(int))
;
```

---

## Strings
> string or String are the same btw<br>Strings are Reference Type but still primitive

```C#
string noval; //will default to null

string s = "amongus";
s.Length; // returns 7
```

besides using `+` operator for concatenating strings, we can also use `string.concat(s1,s2)` 

### string formatting
```java
String.Format("Hello {0} I am {1}", var1, var2);

// is same as

// string interpolation
$"Hello {var1} I am {var2}";
```

**Escape characters**
start with a \ and followed by a character
|character|function|
|-|-|
|`\n`|new line|
|`\"`|render a `"`|
|`\\`|renders a `\`|

**Verbatim Strings**
```C#
string filePath = "C:\\Documents\\test.txt";
//is same as 
string filePath = @"C:\Documents\test.txt"
```
### String equality
```C#
s1 == s2;
// is same as 
s1.Equals(s2);
```

### string comparison
```C#
s1.ToUpperCase() == s2.ToUpperCase();
```

### Immutability of Strings
```C#
string a = "hello";
string b = a;

b = a + "world";

Console.WriteLine(a); // Hello
```

despite being reference type, the expression `a + "world"` created a new string in the heap which b points to.

For programs that require a lot of string concatenation and whatever, it's nice to use **StringBuilder** which modifies strings in a more optimized way.

```C#
using System.Text;
...

StringBuilder sb = new StringBuilder();
sb.Append("Amogus");
sb.AppendLine("sussy");
string s = sb.ToString();
```

### Parsing
```C#
bool b = bool.Parse("true");
double d = double.Parse("3.14");
// might throw exceptions so Try it first

string inp = "true";
if(bool.TryParse(inp, out bool b))
    Console.Write($"b={b}");
```
---
## Methods

### Pass by Reference
by default, method parameters are passed by value. 
```C#
int add(int a, int b){
    return a + b;
}

// like ALU ADD
void ADD(ref int a, int b){
    a += b;
}
```

### out keyword
by default, methods only return a single value. With **out**, multiple values can be returned
```C#
void Test(int a, out int b) {
    b = 10;
    Console.WriteLine($"a={a} b={b}");
}

void Main() {
    int a = 10;
    int b;
    Test(a, out b);
    Console.WriteLine(b); // 10
}
```
> it's like **ref**

<br>

### Using **Params** keyword
captures multiple parameters
```C#
int sum(params int[] values) {
    int sum = 0;
    for (int i = 0; i < values.Length; i++)
        sum += values[i];

    return sum;
}

sum(1,2,3); // returns 6
```

> you can use more than one parameter, but only one can contain the **params** keyword and the one with **params** should always be the last one.

### Named arguments
```C#
int AddNums(int a, int b){
    ...
}

...
AddNums(b:10, a:20);
```

### Expression bodies syntax
```C#
int ADD(int a, int b) => a + b;

ADD(1,2); // returns 3
```
