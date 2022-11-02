# SOLID Principle

Acronym of acronyms (or a macronym) that consists of the following Principles
- **SRP** - Single Responsibility 
- **OCP** - Open Closed 
- **LSP** - Liskov Substitution
- **ISP** - Interface Segregation
- **DIP** Dependency Inversion

> ### Practice PDD (Pain Driven Development)
> Writing your code using the simplest technique you know to get the problem solved. Trying to apply all the SOLID principles upfront is a form of *premature optimization*. Instead, as your application grows, look for places where the app is painful to work with, only then will you assign principles to guide redesign.


# Single Responsibility Principle
Each software module should have one **and only one** reason to change. The individual classes and methods in our applications define what the app does and how it does it.

Multipurpose tools don't perform as well as dedicated tools. Classes should delegate other responsibilities to other objects as much as possible. Dedicated tools are easier to use. A problem with one part of a multipurpose tool can impact all parts

### Coupling, Cohesion, and Concerns
**Tight Coupling** binds two (or more) details together in a way that's difficult to change.<br>
**Loose Coupling** offers a modular way to choose which details are involved in a particular operation.<br>
**Separation of Concerns**; programs should be separated into distinct sections, each *addressing a separate concern*, or set of information that affects the program. High-level code should not know about how low-level implementation details are implemented, nor should it be tightly coupled ot the specific detils.<br>
**Cohesion**; class elements that belong together are cohesive. Cohesion is how closely related elements of a class or module are to one another

Keep classes small, focused and testable

# Open / Closed Principle
software entities (classes, modules, functions, etc) should be open for extension but closed for modification.

It should be possible to change the behavior of a method without editing its source code.

|Open to **extension**|Closed to **modification**|
|-:|:-|
|New behavior can be added<br>in the future|Changes to source or binary code<br> are not required|
|Code that is closed to extension<br>has a **fixed** behavior|The only way to change the behavior<br>of code that is closed to extension is to change the code itself|

Benifits of OCP
- less we need to change the source code, the less likely to introduce new bugs. We also don't need to redeploy
- less likely to break dependent code when we don't have to deploy updates
- fewer conditionals in code that is open to extension results in simpler code

Balancing abstraction and concreteness. Abstraction adds complexity

One good way is to start out by being concrete and wait to see how the app evolves over time; applying abstraction when needed.

### Typcal approaches to OCP
- using parameters; by passing different arguements to a function, we can change its behavior.
- using inheritance; changing the behavior of the underlying type.
- composition / injection; instead of placing the logic directly within a class, the logic is provided by another type by *Dependency Injection*. We can also use **`extension methods`** which can add additional functionality 

# Liskov Substitution Princple
Subtypes must be **substitutable** for their base types. <br> LSP states that *Is-A* relationship is insufficient and should be replaced with *Is-Substitutable-For*

### Classic Rectangle-square Problem
A rectangle has 4 sides and 4 right angles<br>
A square has 4 equal sides and 4 right angles<br>
Per geometry; A square **is a** rectangle

```C#
class Rectangle{
    public virtual int Height { get; set;}
    public virtual int Width { get; set;}
}

class Square : Rectangle{
    public override int Height{
        set {
            Height = value;
            Width = value;
        }
    }

    // Width implemented similarly
}

class AreaCalculator{
    public static int getArea(Rectangle r)
        => r.Height * r.Width;
}
...
// The Problem
Reactangle r = new Square();
r.Width = 4;
r.Height = 5;

AreaCalculator.CalculateArea(r); 
// returns 25 instead of 20
```
The square is not substitutable for the rectangle

LSP Violations:
- type checking with **`is`** or **`as`** in polymorphic code
    ```C#
    foreach(var employee in employees){
        if(employee is Manager){
            Helpers.PrintManager(employee as Manager);
            break;
        }
        Helpers.PrintEmployee(employee);
    }

    // problematic because what if you'll add more subtypes of Employee
    ```
    Type Checking (corrected)
    ```C#
    foreach(var employee in employees)
        employee.Print();

    // or

    foreach(var employee in employees)
        Helpers.PrintEmployee(employee)
    ```
    each subtype should have a different functionality of the same method instead.<br>The 1st implementation violates SLP; use the 2nd
- **`null`** checks; checking for nulls is basically checking the type. **`null`** break polymorphism
- `NotImplementedException`. interfaces are used for abstraction. If you throw this exception, you're basically just saying that *"you can't use this method for this class"* which should've been made clear before compilation and not during run time.

# Interface Segregation Interfaces
*client*s should not be forced to depend on methods they do not use.
> **Client** in this context, is the code that is interacting with an instance of the interface. Also known as the *calling code*

Large interfaces are problematic; it results in more dependencies that result in more coupling which results in more brittle code. It's more difficult to test and deployments.

### ISP violations include:
- Large interfaces
- `NotImplementedException`
- Code uses just a small subset of a larger interface.

Make small interfaces and cohesive with single responsibility to make them distinct and easily distinguishable. You can implement as much interface as you'd need anyways.

# Dependency Inversion Principle
Most classes should depend on abstractions, not implementation details.<br>
Abstraction **should not leak** details. <br>
Classes should be explicit about their dependencies.<br>
Clients should inject dependencies when they create other classes.<br>
**Structure your solutions** to leverage dependency inversion
