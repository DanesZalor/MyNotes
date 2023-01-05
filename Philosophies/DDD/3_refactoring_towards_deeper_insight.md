# Refactoring Toward Deeper Insight

Designing without a model can lead to software which is not true to the domain it serves, and may not have the expected behavior. 

Modeling without feedback from the design and without develoeprs being involved leads to a model which is not well understood by those who have to implement it, and may not be appropriate for the technologies used.

We take time to refactor during the design and developement process because sometimes there is new insight into the domain, something becomes clearer, or a relationship between two elements is discovered. So the design has to be flexible; a stiff design resists refactoring.

When we read the business specifications, we often simplify it; nouns become classes and verbs become methods. But it can often be too simple and lead to a shallow model which lacks depth. And thus we should refactor towards deeper insight.

The software should be more in tune with the way the domain experts think and more responsive to the user's needs.

## Bring Key Concepts into Light

Starting with a coarse, shallow model; we refine it and the design based on deeper knowledge about the domain. As we saw in the sample conversation between the domain expert and the developer, there were multiple refactoring towards the design as more clarity about the domain is expressed.

We need to make implicit concepts explicit. There are implicit concepts, used to explain other concepts which are already in the model. Some of those may play a key role in the design and if so, make those concepts explicit.

There are concepts which are useful when made explicit: constraint, Process and Specification

**Constraint** is a simple way to express an invariant. This is simply done by putting the invariant logic into a constraint.

```C#
class BookShelf{
    private int _capacity;
    private List<Books> _content;

    ...

    public void add(Book b)
    {
        if(_content.Size + 1 <= _capacity)
            content.Add(b);
        
        else
            throw new Exception();
    }
}
```
We can refactor the code, extracting the constraint in a separate method to make it more explicit; easy to read. Everybody will notice that the `add()` is subject to a constraint

```C#
public void add(Book b)
{
    if(!isFull())
        content.Add(b);
    
    else
        throw new Exception();
}

private bool isFull()
    => _content.Size == _capacity;
```

There is room for growth when adding more logic to the methods if the constraint becomes more complex using *Processes*.

**Processes** are expressed in code with procedures. The best way to implement a Process in an object-oriented approach is to use a *Service*. 

If there are different ways to carry out the process, then we can encapsulate the algorithm in an object and use a *Strategy*.

We also have *Specification* which is used to test an object to see if it satisfies a certain criteria.

**For example**: we want to see if a `Customer` object is eligible for a certain credit. The rule can be expressed as a method named `isEligible()` and attatch it to the `Customer` object. But this rule operates on Customer data, see their transaction, loan history, which concerns operations outside the `Customer`'s responsibility. The rule should be encapsulated into an object of its own and be kept in the domain layer.

A single specification checks for simple rules, and then a number of such specifications are combined into a composite one expressing the complex rule like:
```C#
var customer = customerRepo.find(id);

var customerIsElligibleForRefund = new Specification(
    new CustomerPaidDebt(),
    new CustomerHasNoOutstandingBalance());

if(customerIsElligibleForRefund.isSatisfiedBy(customer))
    refundService.issueRefundTo(customer);
```
