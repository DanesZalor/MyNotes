
Resources:
- [Inversion of Control](https://www.tutorialsteacher.com/ioc/introduction)


### What do we mean by "*Dependency*"
```C#
public class A{

    B b;

    public A()
        => b = new B();
    

    public void Task1() {
        // do something here..
        b.SomeMethod();
        // do something here..
    }
}

public class B {

    public void SomeMethod() { 
        //doing something..
    }
}
```

class `A` calls `b.SomeMethod()` to complete its `Task1()`. Class `A` cannot complete its task without class `B` and therefore "Class `A` *is dependent* on class `B`"

The IOC principle suggests to invert the control. Meaning delegate the control to another class. 

```C#
public class A{

    B b;

    public A(){
        b = Factory.GetObjectOfB();
    }

    ...
}
```

### Another example
```C#
public class CustomerBusinessLogic{

    DataAccess _dataAccess;

    public CustomerBusinessLogic()
        => _dataAccess = new DataAccess();
    

    public string GetCustomerName(int id)
        => _dataAccess.GetCustomerName(id);
    
}

public class DataAccess{

    public DataAccess(){}

    public string GetCustomerName(int id) {
        return "Dummy Customer Name"; 
        // get it from DB in real app
    }
}
```
The `CustomerBusinessLogic` class depends on the `DataAccess` class. It creates an object of the `DataAccess` to get the customer data.

`CustomerBusinessLogic` and `DataAccess` are tightly coupled classes because the `CustomerBusinessLogic` includes the reference of the concrete `DataAccess` class. It also creates an object of `DataAccess` and manages the lifetime of that instance.

The problem:

1. `CustomerBusinessLogic` and `DataAccess` are tightly coupled. Changes in the `DataAccess` class will lead to changes in the `CustomerBusinessLogic` as well. If we add, remove, or rename any method in the `DataAccess` class then we need to change the `CustomerBusinessLogic` accordingly.

2. Suppose the customer data comes from different databases or web services and in the future, we may need to create different classes, so this will lead to changes in the `CustomerBusinessLogic` class.

3. The `CustomerBusinessLogic` class creates a **`new`** instance of the `DataAccess`. There may be mutliple classes which use the `DataAccess` and create its objects. So if you change the name of the class, then you need to find all the places in your source code where you created objects of `DataAccess` and change them all. 

4. Because the `CustomerBusinessLogic` creates a new instance of the concrete `DataAccess` class, it cannot be tested independently (TDD). The DataAccess class cannot be replaced with a mock class.

To solve these problems, we can use the **Inversion of Control** and **Dependency Inversion** principles together. IoC is a principle, not a pattern. It just gives high-level design guidelines but does not give implementation details. You are free to implement the IoC priniple *the way you want*.

### Using Factory Pattern to implement IoC

```C#
public class DataAccessFactory{

    public static DataAccess GetDataAccessObj(){
        return new DataAccess();
    }
}
```

Use `DataAccessFactory` in the `CustomerBusinessLogic` class to get an object of `DataAccess` 

```C#
public class CustomerBusinessLogic{

    public CustomerBusinessLogic(){}

    public string GetCustomerName(int id){
        
        var _dataAccess = 
            DataAccessFactory.GetDataAccessObj();
        return _dataAccess.GetCustomerName(id);
    }
}
```

We have inverted the control of creating an object of a dependent class.

