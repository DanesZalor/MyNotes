# Visual Studio

## Terminologies

**Solutions** - open a solution. Holds 0 or more projects. *Create a new solution* when you create a project

**Solution Explorer** - access point to your code. You can also build, run, test, and publish

**Project** - something you are creating that produces an **Assembly**. WebApp, exe, classlib, etc. Will have dependencies from another project or a library from elsewhere. Dependencies between projects are common

**Build Configuration** - gathering of properties to build your project, relating to compiler options and other stuff. You could have one configuration for **release** and one for **debug**. Use them first for now.


<br>

## Debugging 
lets you watch your code execute

**Breakpoint** - stop or pause execution at a particular line of code and look at the state of the application at that very moment like the value of variables.

**Call stack** - see how calls reached that line of code. You can see the call stack when you put a breakpoint in a function.

**Step Over** - you can direct the debugger to execute or step over one line of code.

**Step Into** - step *into a function* and watch it execute line by line. 

**Step out** - run through the rest of this function, pause again once it comes out of the call site

**Continue** - run your application again till the next break point.

**Run to Cursor** - runs the code until it reaches the line where the current cursor is. 

**Immediate Window** - is like an interactive shell for debugging where you can access the variables and shit.

**Autos Window** - you can hover on variables to see their values or you can look at the Autos Window to see or modify their values

## Code viewing

**Go to Definition** - if a function call, opens the file where it is implemented. if a variable, goes to the line of where it is declared

**Peek Definition** - handy little pop-up that peeks the function definition.

**Find all references** - shows where a function is being called.

**Bookmark** - `View -> Bookmark Window`, bookmarking specific line of code from different files

## Code writing

**Intellisense** - assists with code completion

**Refactoring** - rename things, extract constants, reorganize parameters of functions and its calls.

**Format Document** - *code cleanup* based on preferences.

**Snippets** - helps with autocompleting common code blocks like if statements and for loops.

> C# being statically typed may require you to write more code but you don't have to write all that code yourself. Visual Studio offers a lot of tools to help you type and it's easier for a piece of software to help you with it since it's statically typed.

---

## NuGet

- Package manager for .NET
- Reusable code from other developers
- Targeting a known framework version
- Finding its own dependencies

### Dependencies
Under a project (in the solution explorer), you can find `Dependencies->Packages` which will show what libraries that project depends on. <br>

You can right-click on a project and press `Manage NuGet Packages...` <br>

Dependency libraries are NOT in your project or solution folder. They are stored somewhere in `C:/Users/user/.nuget/packages`

You can right click on your solution and press `Manage NuGet packages for Solution...` to see all packages. You can click on the `Consolidate` tab to view the packages that are depended by two or more projects in your solution but with different versions.

### Object Browser

no fckin way you can memorize all that classes and types amirite? go to `View -> Object Browser`