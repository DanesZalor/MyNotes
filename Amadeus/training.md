# training stuff

## Terminologies

**Solutions** - open a solution. Holds 0 or more projects. *Create a new solution* when you create a project

**Solution Explorer** - access point to your code. You can also build, run, test, and publish

**Project** - something you are creating. WebApp, exe, classlib, etc. Will have dependencies from another project or a library from elsewhere. Dependencies between projects are common

**Build Configuration** - gathering of properties to build your project, relating to compiler options and other stuff. You could have one configuration for **release** and one for **debug**. Use them first for now.

<br>

### Debugging 
lets you watch your code execute

**Breakpoint** - stop or pause execution at a particular line of code and look at the state of the application at that very moment like the value of variables.

**Call stack** - see how calls reached that line of code. You can see the call stack when you put a breakpoint in a function.

**Step Over** - you can direct the debugger to execute or step over one line of code.

**Step Into** - step *into a function* and watch it execute line by line. 

**Step out** - run through the rest of this function, pause again once it comes out of the call site

**Continue** - run your application again till the next break point.

## Code Lens

**Go to Definition** - if a function call, opens the file where it is implemented. if a variable, goes to the line of where it is declared

**Peek Definition** - handy little pop-up that peeks the function definition.

**Find all references** - shows where a function is being called.
