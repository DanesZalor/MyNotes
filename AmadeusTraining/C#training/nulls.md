# Working with nulls

Quick review
|Value|Reference|
|-|-|
|`struct`|`class`|
|independent instance|single shared instance|
|value **is** the infornmation|reference **points to** the information|
|No reference, cannot be null|reference may point to "nothing" or **`null`**|
|no need to check for null|null checking sometimes|

### `Nullable<T>` 
Nullable Value Types are instances of the `System.Nullable<T>` struct. This can represent the correct range of values for its underlying value type, plus an additional **`null`** value

```C#

int i  = 10;
bool b = true;

Nullable<int> ni = 10;
Nullable<bool> nb = true;

i = null; 
b = null;
// Compiler Error

ni = null; 
nb = null;
// No Error

ni == null; // evaluates to true
```
> ### Shorthand for nullable
> ```C#
> Nullable<int> x;
> // is same as
> int? x; 
> ```

Nullable variables by default are **`null`**

### Null and Strings
since **`string`** is a reference type, it can be **`null`** which is different from being empty or white space 
```C#
string name = "sex"; 
string name = null; 
string name = ""; // empty
string name = "   "; // whitespeace

// some helpful methods
string.IsNullOrEmpty(name){...}
string.IsNullOrWhiteSpace(name){...}
```

|`Nullable<T>`||
|-|-|
|`.HasValue`| `== null ? false : true`|
|`.Value`| `!= null ? value : throw Exception`|
|`.GetValueOrDefault()`| get value or default|
|`.GetValueOrDefault(default)`| value or specified default|

### Conversions
```C#
int i = 42;
int? j = i; // no explicit cast required

int? i = 42;
int j = i; // error, invalid cast
int j = (int)i; // ok
```

## Null-checking operators
```C#
int x = nullableVar.GetValueOrDefault(-1);
```
is same as the following:
### Conditional Operator
```C#
int x nullableVar.HasValue ? nullableVar.Value : -1;
```

### Null Coalescing Operator
```C#
int x = nullableVar ?? -1;
```

### Null Conditional Operator
let's say we have this situation where we want to assign a nullable property from an obj to a variable:
```C#
SomeObject obj = null;
int x; // = obj.nullableVar;
```

normally we'd do something like this
```C#
if(obj != null)
    x = obj.nullableInt;
else
    x = -1; // user-defined default value
```

but we can do this instead
```
x = obj?.nullableInt ?? -1;
```

We can also use it for arrays;
```C#
SomeObject[] objs = null;

string n1 = objs?[0]?.Prop1; 
string n3 = objs?[3]?.Prop1; 
```

## Eliminating Null Reference Exceptions

> ### Null Object Pattern
> A software design pattern that uses object-orientation to remove or reduce the amount of null references and thus reduce the burden of repetitive null checking and handling code in specific parts of the code base

Add a static Property in a class that represents the null with a *"do nothing"* implementation. idk bro just watch the [course](https://app.pluralsight.com/course-player?clipId=0e6e71a2-438b-4a47-9879-20bc47fce0f7) i don't wanna copy it here

## Non-Nullable Reference types
```C#
#nullable enable
string message = null;
#nullable disable
```

or we can set it project wide in our `.csproj` file
```xml
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
    ... some stuff about whatever
    <Nullable>enable</Nullable>
</PropertyGroup>
</Project>
```


