## Dependency Inversion Principle

> #### Definition
> 1. High-level modules should not depend on low-level modules. Both should depend on the abstraction
> 2. Abstractions should not depend on details. Details should depend on abstractions.

Consider the previous Example
```C#
class CustomerBusinessLogic{

    public CustomerBusinessLogic(){}

    public string GetCustomerName(int id){
        DataAccess _dataAccess = 
        DataAccessFactory.GetDataAccessObj();
        return _dataAccess.GetCustomerName(id);
    }
}

class DataAccessFactory{
    public static DataAccess GetDataAccessObj()
        => new DataAccess();
}

class DataAccess{
    public DataAccess(){}

    public string GetCustomerName(int id)
        => return "Dummy Name";
        // get it from DB in real app
}
```

We implemented factory pattern to achieve IoC. But the `CustomerBusinessLogic` still uses the concrete `DataAccess` and thus it is still tightly coupled.  

As per the DIP definition, *"a high-level module should not depend on low-level modules. Both should depend on abstraction"*

A high-level module is a module is one that depends on other modules. `CustomerBusinessLogic` depends on `DataAccess` so the `CustomerBusinessLogic` is the high-level module and the `DataAccess` is the low-level module.

```C#
interface ICustomerDataAccess{
    string GetCustomerName(int id);
}

class CustomerDataAccess: ICustomerDataAccess{
    public CustomerDataAccess(){}

    public string GetCustomerName(int id)
        => "Dummy Customer Name";
}

class DataAccessFactory{
    public static ICustomerDAtaAccess GetCustomerDataAccessObj()
        => new CustomerDataAccess();
}

class CustomerBusinessLogic{
    ICustomerDataAccess _custDataAccess;

    public CustomerBusinessLogic(){}

    public string GetCustomerName(int id)
        => _custDataAccess.GetCustomerName(id);
}
```

Now both `CustomerBusinessLogic` and `CustomerDataAccess` communicate with each other through abstraction. 