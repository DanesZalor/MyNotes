# Defensive Coding

to better prepare our code for the perils of the real world and real users.

### What are we defending our code from?

#### 1. **Incorrect Entry**
our users are depending on our app to produce correct results, which needs the user to input correct data. We defend our code against incorrect entry by adding appropriate user **entry validation**.

#### 2. **Invalid operations**
to produce valid results, we must pass accurate data into our methods so that they can correctly perform their operations. We protect our code from invalid operations by checking the **arguments** passed into those methods and by fully unit testing the operations

#### 3. **System mishaps**
with software, there's always something that can go wrong such as losing connectivity when they attempt to save their data, or storage device used for logging user action suddenly fails. We protect our code from these mishaps by adding **checks** and **manage exceptions** like checking if the network is available before saving, throw an exception if it fails, then save the data locally until the network is reconneceted.

#### 4. **Future developers**
including ourselves that may not remember why we added that particular line of code. If our code is not clear and another developer (such as our future selves) doesn't understand our intent, they might make incorrect assumptions and make inappropriate changes. We defend our code against future developers by writing **clean code** and by having a thorough set of **unit tests** so that they could rerun it and check easily whether it works

*"Anything that can go wrong will go wrong"* - Murphy's Law

### Defensive Progrramming
"is an approach to improve software and source code, int erms of
- General *`quality`* - reducing the number of software bugs and problems.
- Making the source code *`comprehensible`* - the source code should be readable and understandable, so it is approved in a code audit.
- Making the software behave in a *`predictable`* manner despite unexpected user inputs or user actions."

 ### Defensive Coding Helps us improve
 - **Code comprehension** - the easier it is to understand, the easier it is to modify and maintain. It also has clear intent which minimizes incorrect modifications, better protecting our code from changing requirements, and multiple developers over time.

    Improve Code comprehension by:
    - writing code that is clean and easy to read.
    - Single responsibility principle
    - Separation of concerns
    - Don't repeat yourself (DRY)
<br><br>

 - **Code quality** - through automated code tests that exercise each logical unit of the application, it helps us evaluate the quality of our defenses and we can run the tests after each code change protecting the application by affirming its operations are not adversely impacted by the change.

    Improve Code Quality by
    - Building unit tests
    - Re-execute tests after each modification
<br><br>

 - **Code predictability** - through user validation, clearly-defined method inputs and outputs, and exception management. No matter what goes wrong, despite user errors and unforeseen circumstances, our application protects itself and continues successfully.
    
    Improve Code predictability by:
    - Principle of Least Surprise
    - Validate method arguments
        - define a clear method signature
        - fail fast with guard clauses
        - refactor for separation of responsibilities
    - Handle nulls
        - use nullable value types as needed
        - guard against null nullable value types
        - guard against null reference types
        - use nullable and non-nullable reference types
        - return predictable results
            - return a value when expected
            - return a nullable type as needed
            - consider returning a tuple or object instead of throwing exceptions
        - manage exceptions
            - define an exception management strategy
            - throw appropriate .NET exceptions
            - create and throw custom exceptions as needed
            - catch what you're thrown
 ## Conclusion

