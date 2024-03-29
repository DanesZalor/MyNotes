# C# .NET Quick Refresher

### Quickstart
create a new **dotnet console** project
```bash
dotnet new console -n dirname
```

#### Hello World
```C#
public class Test{

    public static void Main(string[] args){
        Console.WriteLine("せかいこんいちは");
    }
}
```

#### Run the project
```bash
dotnet run
```

## Functions

### Default arguements
```C#
void F1(int x=1, float y=3.1f){
    Console.WriteLine(
        String.Format("x={0} y={1}", x,y)
    );
}

...
F1();
F1(y:6.9f);
```
Outputs
```bash
x=1 y=3.1
x=1 y=6.9
```


## Classes

### fields and properties

```C#
public class Vector2{

    protected float _x, _y;

    public float X {
        get => _x;
        set => _x = value;
    }

    public float Y {
        get => _y;
        set => _y = value;
    }

    public Vector2(float x=0f, float y=0f){
        this.X = x;
        this.Y = y;
    }
}
```
`_x` is a field while `X` is a property.

### Inheritance
```C#
/**
 * Vector2 but Y will always be >= 0 
*/
public class UpVector2 : Vector2 {

    public override float Y{
        get => this._y;
        set {
            if(value<0) 
                Console.WriteLine("Warning! UpVector2.Y is always >= 0");
            this._y = Math.Max(0,value);
        }
    }

    public UpVector2(float x=0, float y=0) : base(x,y) {}

}
```

> **sub : base()** to invoke the base class constructor

> private variable cannot be accessed by the subclass BUT still inherited (can access via some methods)


### method override
a method must be **abstract** or **virtual** in order to be **override**

**abstract** should not be  implemented while **virtual** is

> **Polymorphism** multiple forms that inherit the same base class. Can be treated as the base class like storing them in an array and calling a method that is implemented differently based on what form (or subclass) it is

## sealed and abstract

**sealed** - classes that cannot be derived<br>
**abstract** - classes that cannot be instantiated so it must be derived in order to instantiate

# Interfaces

define a contract that must be implemented by classes that implements it

CONVENTIONALLY contain no implementation code <sub><sup>but it's possible</sub></sup>. 

conventionally starts with an "I" like `IEmployee`

```C#
public interface IInterface{
    void SomeMethod();
    double SomeOtherMethod();
}
---
public class Class : IInterface{
    ...

    void SomeMethod(){ ... }

    double SomeOtherMethod(){ ... }
}
```

kind of abstract class? except in C#, you can only inherit one base class (unlike C++), BUT *you can implement more than 1 interface*

```C#
public class Class : Interface1, Interface 2 {...}
``` 

### Commonly used interface
built in interfaces that are commonly used:
- `IComparable` for sorting
` `IEquatable` to check equality between 2 objects
- `ICloneable` for cloning
- `IEnumerable` for elements in a list
- `IList` for indexable objects like a LinkedList
- `IDisposeable` disposeable unmanaged resources

Example

Say you have an `Employee` object that you want to compare with other instances of `Employee` to sort them:
```C#
public class Employee : ICompareable, IEmployee {
    ...
    private int Id;
    ...

    public int CompareTo(object obj)
    {
        var otherEmployee = (Employee)obj;
        if (Id > otherEmployee.Id)
            return 1;
        else if (Id < otherEmployee.Id)
            return -1;
        else
            return 0;
    }
}

... somewhere in your code ...

List<Employee> emps = new List<Employee>();
// ... some add to list calls
emps.Sort(); // sort based on CompareTo()
```

Interfaces also provide polymorphic behaviour

```C#
public class Manager : Employee { ... }

...
IEmployee e1 = new Manager();
e1.Work(); // valid
e1.AttendManagementMeeting(); // error: can only call IEmployee methods
```
<br>

`IEnumerable<T>` interface
allows the collection to act as a data source

`T[]` and `List<T>` both have almost the same set of features and that's because they both implement `IList<T>` which provides functionalities such as being indexable, enumerable, etc.

> It's often preferred to use interfaces instead of concrete types.


----
# oop <sub><sub><sup><sup>(from pluralsight course)

an approach to designing and building apps by treating the problem like they consist of objects

- identify class
- separate responsibilities
- establish relationships between objects
- leverage use

> ### Abstraction
> process of simplifying things by ignoring irrelevant details to the problem and focusing on waht is important
> ### Encapsulation
> hide or encapsulate implementation details within a class; hiding complexity. Like hiding some properties or methods that does not concern other classes and just exposing those that are needed

**Common App Layers**
- **UI Layer** - where the user interacts 
- **Business Logic** - layer where to perform business operations
- **Data Access** - retrieve data from a repository
- **Common Code/Lib** - useful code project-wide

### Terminologies
- **Method Signature** - method name and data types of parameters
- **Overloading** - having multiple functions w the same name but different parameter/s
- **Contract** - interfaces and rules and shiet


### Identifying classes
- represent business entities
- define properties (data)
- define methods (actions/behavior)

### Separating Responsibilities
an app is decomposed into classes with minimal overlap. each class is responsible for a separate concern
> **YAGNI** - "*You aren't going to need it*". Principle that focuses on what is important for today. 
- minimizes coupling<br>
    *coupling* is a degree to which classes are dependent on other classes or external resources. Ideally should minimize a class' dependency. 
- maximizes cohesion<br>
    *cohesion* is a measure of how related everything in a class is to the purpose of the class

Classes with both low coupling and high cohesion are easier to understand, test, maintain and extend.

### Establishing Relationships
- define how objects work together to perform the operation of the application
- types of relationships
    - **Collaboration** ("*uses a*") - one object uses another object to establish a process
    - For example; An `API` that *uses a* `SQLRepository`. The `ResourceRepository` may be used by other classes and the `API` can exist without an `SQLRepository`  
    - **Composition** ("*has a*") 
        - An object is composed of other objects
        -  two categories:
        - **Aggregation** - when an object is composed by another object exists outside of the relationship. For example; a `Car` and it's `Wheel[]`. Ideally, A Wheel
        - **Composition** - when an object is composed of another object but that object can't exist without the other. For example; A `Bird` and it's `Wing[]`
        > medjo bad example go find something man
