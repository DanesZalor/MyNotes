# C# Generics

What if you want to make a data structure like a stack and you want to use it for different data types?
```C#
public class Stack<T>{

    private readonly T[] _items;
    private int _currIdx = -1;

    // for example's sake lets just make it 10
    public Stack() => _items = new T[10];

    public int Count => _currentIdx + 1;

    // for example's sake let's ignore the possible IndexOutOfRangeException
    public void Push(T item) => 
        _items[++_currIdx] = item;
    
    public T Pop() =>
        _items[_currIdx--];
}
...

var stack = new Stack<int>();
stack.Push(2);
stack.Push("sex"); // compiler error

stack = new Stack<string>();
stack.Push("sex");
stack.Push(420.69); // compiler error
```

> If you use `object` instead it compromises Type-safety and performance (has un/boxing) like casting.
> 
> ### Advantages of Generics
> - Code reuse
> - Type-safety
> - Performance (no un/boxing)

> ### `System.Collections.Generic`
> 
> Contains a lot of Generics usually data structures like `List<T>`, > `Dictionary<T>`, `Stack<T>`, etc. 

### Generic Class Inheritance

```C#
class intStack : Stack<int>
{
    public void PrintAllOdds(){ ... }
}
```

```C#
class AdvancedStack<T> : Stack<T> 
{
    public void Clear();
    public void RemoveAt(int idx){ ... }
    public void Remove(T item){ ... } 
} 
```

### Multiple Type Parameters
```C#
class CustomTuple <T1, T2, T3> { ... }

class CoolerTuple <T1,T2, T3> : CustomTuple <T1, T2, T3> { ... }
```
> the typeholder such as `T1`, `T2` can be any name

### Generic Type Constraint
Constrain the type to a class. Useful for base class with polymorphs so you can access the base class variables.
```C#
class Entity{
    public int Id {get; set}
}

class Repo<T> where T:Entity {

    private List<T> _repo = new(); 

    public T GetById(int id){

        // for example's sake, ignore the possible Exception thrown by .Single()
        return _items.Single(item => item.Id == id);
    }
}
```

or you can use Interface constraints

```C#
interface IEntity {
    public int Id {get; set; }
}

class Generic<T> where T : IEntity { 
    ...
    // you can use IEntity.Id
}
```

## Generic Interface

> ### Dependency Inversion Principle
> Components must depend on **abstractions** and **not implementations**

```C#
// class restriction 
interface IRepository<T> where T : class {
    void Add(T item);
    IEnumerable<T> GetAll();
}

ListRepository<T> : IRepository<T> { ... }
SQLRepository<T> : IRepository<T> { ... }
```

## Interface Inheritance
```C#
interface IRepo<T> where T : IEntity { ... }

class Person : IEntity { ... }

interface ISuperRepo<T, Tkey> : IRepo<T> where T : Entity { ... }

interface IPersonRepo : IRepo<Person> { ... }
```

## Generic Method
```C#
void AddBatch<T>(IRepo<T> repo, T[] items)
where T : IEntity
{
    foreach(var item in items)
        repo.Add(item);
}
...
AddBatch<Employee>(employeeRepo, employees);
```

### Method extension
```C#
public static class RepositoryExtensions
{
    public static void AddBatch<T>(this IWriteRepository<T> repository, T[] items)
    {
        foreach (var item in items)
        {
        repository.Add(item);
        }
        repository.Save();
    }
}
... 
IWriteRepository employeeRepo = new EmployeeRepository();

employeeRepo.AddBatch(...);
```

```C#
using System.Text.Json;

public static class EntityExtensions
{
    public static T? Copy<T>(this T itemToCopy)
    where T : ISomething {
        var json = Json.Serializer<T>(itemToCopy);
        return JsonSerializer.Deserialize<T>(json);
    }
}
```

## Delegate

### Non-generic Delegate
```C#
public delegate void MyDelegate(string msg);

public void MyMethod(string msg){
    Console.WriteLine($"MyMethod:{msg}");
}

... 

MyDelegate del = (string msg) 
    => Console.WriteLine($"MSG:{msg}");

del.Invoke("yo wassap"); // or del("")

del = MyMethod;
del("yoooo");
```

### Generic Delegate
```C#
public delegate T Operate<T>(T a, T b);

...
var ADD = (int a, int b) => a + b;
Console.WriteLine(ADD(2,3)); 

var concat = (string a, string b) => a + b;
Console.WriteLine(concat("among", "us"));
```

> **`Action`** is a delegate (pointer) to a method, that takes zero, one or more input  parameters, but does not return anything.
> <br>**`Func`** is a delegate (pointer) to a method, that takes zero, one or more input parameters, and returns a value (or reference).

```C#

delegate void Procedure();
...

public void Func1() =>
    Console.WriteLine("Func1() call");

public void Func2() =>
    Console.WriteLine("Func2() call");

public void Func3() => 
    Console.WriteLine("Func3() call");

...
Procedure someProcs = Method1;
someProcs += Method2;
someProcs += Method3;

someProcs();
```
```
Method 1
Method 2
Method 3
```


