# Exceptions

> why catch exceptions? <br>
> Besides not crashing, we could
> - chance to fix/retry
> - meaningful error messages and graceful exit
> - opportunity to log errors 
> > good error handling code helps future maintainers understand what possible error conditions may occur and how they can be handled 

### Error Handling using Error Code

- need to know all 
     - the return values that represent errors
    - return values that represent success
- need to remember to add an else if / switch statements for every return value

Exceptions can provide more readable code and less clutter. Exceptions can bubble up in a stack trace which is helpful

> ## Exception
> is any error condition or unexpecte behavior that is encountered by an executing program.

```C#
Exception
|- System.Exception
|  |- OutOFMemoryException
|  |- StackOverflowException
|  |- ArgumentException
|  |  |- ArgumentNullException
|  |  |- ArgumentOutOfRangeException
|- ArithmeticException
|  |- DivideByZeroException
|  |- OverflowException
|- ApplicationException
|- (custom Exceptions)
```

|`System.Exception`||
|-|-|
|Message : `String`|Describes the reason for the exception<br>Should describe the rror and how to correct (if applicable)|
|StackTrace : `String`|Information about call stack;<br> Trace of method calls leading to exception|
|Data : `IDictionary<string,object>`|Additional user-defined exception data|
|InnerException : `System.Exception`|Capture preceeding exception in new exception; *Exception wrapping*|
|Source : `String`|Application/object name that caused error<br>Defaults to name of originating assembly|
|HResult : `Int32`|Represents a HRESULT numerical value<br>Often used with COM-interop|
|HelpLink : `String`|Link to associated help file|
|TargetSite: `System.Reflection.MethodBAse`| Method that threw current exception <br>`{Name, Return type, access mod, etc.}`|

> ### ApplicationException GuideLines
> - It should not be thrown by your code
> - it should not be caught (unless you rethrow the original exception)
> - Custom exceptions should not be derived from this


### Exception Wrapping
```
public Exception(string? msg, Exception? InnerException)
```
```C#
throw new Exception(
    "Message", 
    new System.IndexOutOfRangeException(
        "Inner Message", 
        new Exception()
    )
);
```

### Commonly Encountered Exceptions
- ### Exception & SystemException
    - `Exception`: Represents execution errors
    - `SystemException`: Base class for for exceptions in system exceptions namespace
    - You don't throw them
    - You don't catch (except in top-level handlers)
    - Don't catch in framework code (unless you rethrow)
- ### InvalidOperationException
    - Thrown when the current state of the object is invalid for a specific method being called
    - Throw when your object is in an inappropriate state when a method is called
- ### ArgumentException, ArgumentNullException, ARgumentOutOfRangeException
    - `ArgumentException`: Thrown when a method argument is invalid (base class)
    - `ArgumentNullException`: thrown when a null is passed to a non nullable method arguement
    - `ArgumentOutOfRangeException`: thrown when a method argument is outside of an allowable range
- ### NullReferenceException & IndexOutOfRangeException
    - `NullReferenceException` thrown when an attempt is made to dereference a null object reference
    - `IndexOutOfRangeException`: Thrown when attempting to index an `IEnumerable<T>` out of bounds
    - Reserved for runtime use
    - usually indicate a bug in the program
    - Do not throw
- ### StackOverflowException
    - thrown when too many nested method calls 
    - reserved and thrown by runtime
    - do not explicity throw
    - do not catch
    - usually impossible to correct
- ### OutOfMemoryException
    - when there is not enough memory to continue executing the program
    - reserved and thrown by run time
    - do not explicitly throw

## Exception Handling
You have to handle exceptions from the *most specific to the least*
```C#
try{
    // some operation
}catch(ArgumentNullException e){
    // handle ArgumentNullException exception
}catch(InvalidOperationException e){
    // handle InvalidOperationException exception
}catch{
    // handle other exceptions
}finally{
    // executed after the control leaves the try block
    // or the exception is handled
}
```

## Exception Handling Good Practices
- do not add a catch block that does nothing or just rethrows
    - catch blocks should add some value
    - may be used to log the error
    - bad practice to ignore or swallow exceptions
- Do not use exceptions for normal program flow logic
    - e.g input validation
        - you except input to be invalid sometimes
        - not an exceptional situation
        - part of expected logic flow
    - isValid(x) methods
- design code to avoid exceptions in the first place
    - use TryParse() instead of Parse()
    - consider returning null (or null object pattern) for extremely common errors
- use correct grammar in exception messages
- use finally blocks for cleanup
    - like calling Dispose()
    - callers of method should be able to assume no unexpected side effects when exception thrown/caught

### C# Throw exception in expressions
```C#
string test = arg ?? throw new ArgumentNullException(nameof(arg)); 
```

### Catch filtering
```C#
catch(ArgumentNullException e) when (e.ParamName == "operation"){...}
```

### Handling exception globally
it depends on app output such as Console, Web, etc.
```C#
AppDomain.CurrentDomain.UnhandledException += new UnhandledExceptionEventHandler(...);
```

## Custom Exception
- Use existing .NET exception types where applicable like:
    - `InvalidOperationException` if property set/method call is not appropiate for current state
    - `ArgumentException` (or derived) for invalid parameters
- Wrap inner exception if appropriate
- don't use custom (or existing) exceptions for normal (non exceptional) logic flow

- Only use when:
    - they need to be caught and handled differently from existing exceptions
    - e.g want to perform special monitoring of a specific critical exception type
    - building a lib/framework for use by other developers so consumers can react to errors in your library
    - interfacing with external API, DLL, service

- Implementing
    - Naming convention: `...Exception`
    - implement the standard 3 constructors
    - add additional properties where needed
    - never inherit from `ApplicationException`
    - inherit from `Exception` or your other custom exception
    - keep the number of custom exception to a minimum

for example
```
| System.Exception
| |- JsonException
| |  |- JsonReaderException
| |  |- JsonSerializationException
| |  |- JsonWriterException
```

```C#
class CalculationException:Exception{
    
    const DefaultMessage = "An error occured during calculation";

    public CalculationException() 
    : base(DefaultMessage) {...}

    public CalculationException(string msg) 
    : base(msg) {...}

    public CalculationException(Exception inner) 
    : base(DefaultMessage, inner) {...}

    public CalculationException(string msg, Exception inner) 
    : base(msg, inner) {...}
}
...

try{
    return arg1 / arg2;
    catch(ArithmeticException e)
    {
        throw new CalculationException(e);
    }
}
```


