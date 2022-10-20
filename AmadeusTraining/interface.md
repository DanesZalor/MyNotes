# Interface

is like a contract that dictates *"I have these functions"*

Can also help with Polymorphism by using the Interface instead of a base class

Let's say someone else's code has this thing
```C#
class Person : IEntity { ... }
class PersonModel{
    ...
    public static Person[] getAll(){ ... }
}
```

And you use that code in your code like
```C#
IEntity people = Person.getAll();
```

If however they change `Person.getAll()`'s return method to `List<Person`, you don't have to change your code

> Different Data Sources include
> JSON, CSV, SQL, Cloud Service, Azure, etc.
> ## Repository Pattern
> Mediates between the domain and data mapping layers using a collection-like interface for accessing domain objects. <br>
> Separates our application from the data storage technology. <br> We do not want our app code to know how to make HTTP calls or open a file system. Instead, a **Repository** is responsible for those details
> 
> ### Factory Method Pattern
> A single class that can access all the repository types


```C#
public interface IPersonRepository{
    void Add(Person p);
    IEnumerable<Person> GetAll();
    Person Get(int id);
}
```
Using this interface we can then implement other Repositories that implement this interface such as
```C#
public class SQLRepo : IPersonRepository {
    void Add(Person p){ 
        /* add to Database*/ 
    }
    IEnumerable<Person> GetAll(){ 
        /* fetch all from db*/ 
    }
    void Get(int id){
        /* fetch row from db with id = id*/
    }
}

public class WebAPIRepo : IPersonRepository{
    const baseURI = "http://server:port/api/"
    void Add(Person p){ 
        /* POST baseURI+"items" */ 
    }
    IEnumerable<Person> GetAll(){ 
        /* GET baseURI+"items"*/ 
    }
    void Get(int id){
        /* GET baseURI+"item"*/
    }
}

public class CSVRepo : IPersonRepository{
    File filename;

    private string Serialize(Person p){ ... }

    void Add(Person p){ 
        /* deserialize p and append */ 
    }
    IEnumerable<Person> GetAll(){ 
        /* get line by line 
         * foreach line, serialize into Person
         * 
        */ 
    }
    void Get(int id){
        /* GET baseURI+"item"*/
    }
}

// and other Repository Types

// and then we can use all these like

IPersonRepository ipr = new CSVRepo();
IPersonRepository ipr = new SQLRepo();

// so we can just use the IPersonRepository methods instead of the CSV or SQL
```

> ### Interfaces for **Dynamic Loading**
> This is also useful for dynamic loading; getting the repository type from a config file instead of determining it in compile time
> ```C#
> public static IPersonRepository getRepo()> {
>    string repoTypeName = ConfigurationManager.AppSettings["RepositoryType"];
>
>   // create an instance of the repoType
>    Type repoType = Type.GetType(repoTypeName);
>    object repo = Activator.CreateInstance(repoType);
>
>    IPersonRepository personRepo = repo as IPersonRepository;
>
>    return personRepo;
>}
>```
> <br>

Interfaces help us with *separation of concerns* and puts responsibilities where they belong



## Implicit and Explicit Interface Implementation

let's say we have this interface
```C#
public interface ISaveable{
    void Save();
}
```
### Standard (Implicit) 
```C#
public class Catalog : ISaveable{
    public void Save(){
        Console.WriteLine("Saved");
    }
}

...
Catalog c new Catalog(); 
c.Save(); // "Saved"

ISaveable s = new Catalog();
s.Save(); // saved
```

### Explicit 
```C#
public class Catalog : ISaveable{
    public void ISaveable.Save(){
        Console.WriteLine("Saved");
    }
}

Catalog c new Catalog(); 
c.Save(); // Compiler Error

ISaveable s = new Catalog();
s.Save(); // "Saved"
```

This forces someone to use the interface instead of the concrete class if they wanted to access certain functionalities

It's also possible to have multiple implementations
```C#
public class Catalog : ISaveable{
    public void Save(){
        Console.WriteLine("Saved (catalog");
    }

    public void ISaveable.Save(){
        Console.WriteLine("Saved (interface)");
    }
}
```

We can have even more implementations from other implemented interfaces with different return types
```C#
public interface ISaveable{
    void Save();
}

public interface IDbSaver{
    string Save();
}
```

### Interface Drawbacks
When we try to `Go To Definition` on an interface method, it will go to the unimplemented code. If we `Go To Implementation` it can't find the implementation since it's unimplemented in the interface. So in order to track which implementation is being used, we have to use the debugger which takes more time

> ### Interface Segregation Principle
> Clients should not be forced to depend upon methods that they do not use. Interface belong to clients, not to hierarchies. <br>
>
> Interfaces should only include what the calling code needs.

We can make use of **Interface Inheritance** 

```C#
public interface IPersonReader {
    Person Get(int id);
    IEnumerable<Person> GetAll();
}

public interface IPersonRepository : IPersonReader {
    void Add(Person p);
    void Update(int id, Person np);
    void Delete(int id);
}
```

this can create levels of access. A lower level access of the Person Data Source could just inherit `IPersonReader` while a high level access can inherit `IPersonRepository`

### Interfaces vs Abstract Classes

|Interface|Abstract|
|-|-|
|No implementation|May implement code|
|multiple inheritance|strictly single inheritance|
|members automatically public|access modifiers|
|properties, methods, events, indexers|in addition; fields, constructors and destructors|

Example
```C#
Polygon
    
// shared implementation
int NumOfSides{...}
double GetPerimeter()

// unique implementation
abstract double GetArea()
```
> with so much shared code, it's better to use Abstract class

```C#
PersonRepository

// all these methods have unique implementation
// for CSV, SQL, or WEB repository
IEnumerable<Person> GetPeople();
Person GetPerson(int id);
void Delete(int id);
```
> with no shared code, it's better to use implementation

<br>

## Interfaces in Frameworks and Patterns

> ### Dependency Injection
> set of software design principles and patterns that enable us to develop loosely coupled code. With loose coupling, our code is easier to maintain, extend and test.

> ### Decorator
> wrapping an existing interface and then exposing the same interface in the outside
> <br>Example:<br>
> We have a `WebRepository` that accesses a *Web Service* which returns a JSON and is serialized by `WebRepository`. We can create a `Caching Repository` that adds a client-side cache to our existing repo. Our `Caching Repository` wraps in our existing repository which implements all methods. When it calls `GetPeople()` it calls the `WebRepository.GetPeople()` on top of it's own implementation. It can be used to add logging, authorization, etc. 

> ### Mocking
> creating an in-memory object for testing purposes. We can make a `FakeRepository` project for testing but it can get messy based on the project's scope. Instead we can use the mocking framework like `MOQ` which is available as a NuGet package

