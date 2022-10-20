# [LINQ (Language Integrated Query)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/linq/introduction-to-linq-queries?source=recommendations)

integrating query capabilities into C#

```C#
int[] scores = { 97, 92, 81, 60 };

IEnumerable<int> passingScores = 
    from score in scores where score > 80 select score;

foreach(int i in passingScores) Console.Write(i + " ");
```
`passingScores` becomes `{97, 92, 81}`.

```C#
// Data Source
int[] nums = {3,4,5,6,7,8};

int[] div3 = (
    // Query Creation
    from num in nums where num%3==0 select num
).
// Execution
ToArray<int>();
```
`div3` becomes `{3,6}`

The query  expression contains three clauses: `from`, `where` and `select` where `from` specifies the data source, `where` applies the filter, and `select` specifies the type of the the returned elements.

The query itself only returns the query commands. The actual execution of the query is deferred until you iterate over the query variable in a `foreach` statement. 

Using `Count`, `Max`, `Average`, `First`, `ToArray` will force immediate execution. 

```C#

public class Student
{
    public string? Name { get; set; }
    public int[]? Scores;
}
...

Student[] students = {
    new Student{Name="Bob", Scores=new int[]{90,80,71} },
    new Student{Name="Dan", Scores=new int[]{90,90,70} },
    new Student{Name="Jam", Scores=new int[]{90,70,70} },
    new Student{Name="Jim", Scores=new int[]{80,70,70} },
    new Student{Name="Pam", Scores=new int[]{80,70,70} },
};

Student[] failingJs = ( 
    // Student whose name starts with J and has an Average score <80
    from s in students 
    where s.Scores.Average() < 80 && s.Name.StartsWith("J")
    select s
).ToArray<Student>();

foreach(Student s in failingJs) 
    Console.WriteLine(s.Name + " ave.="+ s.Scores.Average());
```
Outputs
```
Jam ave.=76.66666666666667
Jim ave.=73.33333333333333
```

<br>

# C# Linq <sub><sup>from course</sub></sup>

SQL-like syntax in C# (and VB). It allows us to query `IEnumerable<T>` or those that implements it. We can also Query external data sources (xml, database, JSON, csv, etc)

|Common `IEnumerable`|
|-|
|array|
|string|
|List<T>|
|HashSet<T>, Dictionary<Tkey,Tval>, etc|

|SQL|LINQ|Method|
|-|-|-|
|`SELECT * FROM Products`|`from prod in Products select prod`|`Products`<br>`.Select(prod => prod)`|
|`SELECT Name FROM Products`|`from prod in Products select prod.Name`|`Products`<br>`.Select(prod => prod.Name)`
|`SELECT * FROM Products WHERE ListPrice > 10`|`from prod in Products where prod.ListPrice > 10 select prod`|`Products`<br>`.Where(prod=>prod.ListPrice>10)`<br>`.Select(prod => prod)`|


## Select & Order operations

```C#
List<Product> Products; // some populated list
List<Product> list;

// Query Syntax
list = (from prod in Products select prod).ToList();

// Method Syntax
list = Products.Select(prod => prod).ToList();
```

### Selecting a single column
```C#
from item in Items 
select items.Column

// is equal to 

Items.Select(item => item.Column);
```

### Get Specific ColumnS

```C#
from prod in Products
select new Product { 
    ProductID = prod.ProductID,
    Name = prod.Name,
    Size = prod.Size,
}
---
// or use an AnonymousClass
var list = (from prod in Products
select new { 
    ProductID = prod.ProductID,
    Name = prod.Name,
    Size = prod.Size,
});

foreach (var prod in products)
{
    Console.Write($"Product ID: {prod.Identifier}");
    Console.Write($"      Name: {prod.ProductName}");
    Console.Write($"      Size: {prod.ProductSize}");
}
----
// method form
Products.Select(prod => new{
    Identifier = prod.ProductID,
    ProductName = prod.Name,
    ProductSize = prod.Size,
});
```
> Anonymous Class must be used within the same block of code

### Ordering data using LINQ

```C#
from item in list
orderby item.Property
select item

// or

list.OrderBy(item => item.Property)
```

#### Descending order

```C#
from item in list
orderby item.Property descending
select item

// or

list.OrderByDescending(item => item.Property)
```

#### Order by multiple fields

what if you want to order a list by a property, and then those in the same order would be ordered by another property

```C#
from item in list
orderby item.Property1 descending, item.Property2
select item

// or

list
.OrderByDescending(item => item.Property1)
.ThenBy(item => item.Property2)
```

### Extract Data using Filtering and Element operations

fetch multiple items that fit the **`where`** filter

```C#
from item in list 
where item.Property1 == value1 &&
item.Property2 > value2
select item

// or

list.Where(item => item.Property1 == value1 && item.Property2 > value2)
```

#### Custom Extension Method
```C#
public static class ListHelper{
    public static IEnumerable<Item> ByProp1(
        this IEnumerable<Item> query, string prop1
    ){
        return query.Where(item => item.Prop1 == prop1);
    }
}

---
(from item in list select item).ByProp1(prop1)
```

#### Select Single Item
```C#
var val = (from item in list select item)
.First(item => item.Property == search);

// or

var val = list.First(item => item.Property == search);  

// if it finds the first item that matches the lambda criteria it will put that in the val 

// it will throw an exception if it doesn't find anything

// we can use .FirstOrDefault() instead. If it doesn't find anything, it will just return null
var val = (from item in list select item)
.FirstOrDefault(item => item.Property == search)
```

> `.Last()` and `.LastOrDefault()` exists works the same way<br>
> `.Single()` and `.SingleOrDefault()` works the same as well BUT it throws an exception if there's multiple matches

## Set Operations
Iterate over entire collection, set a property value in collection like `SQL UPDATE`

```C#
from item in list
let tmp = item.AssignHere = item.FromHere
select item

// or

list.ForEach(item => item.AssignHere = item.FromHere)
```

### Sum

```C#
...
Item[] items = {
    new Item("Yakult", 5f),
    new Item("Milk 2L", 15f),
    new Item("Milk 3L", 20f),
    new Item("Tonkatsu", 6f)
};

float x = items
.Where(item => item.Name.StartsWith("Milk"))
.Sum(item => item.Price); 
// 35
```

### `.Distinct()`

```C#
foreach(int p in items.Select(item => item.Price).Distinct()) 
    Console.WriteLine(p);
```

### `.All()`
```C#
items.All(item => item.Price > 0); // returns true
items.All(item => item.Price > 5); // returns false
```

> `.Any()` works how you'd expect 

<br>

## Comparing Objects

### Sorting
```C#
class Vec2 : IComparable, IEquatable<Vec2> {
    public float x, y;
    
    public float Magnitude{
        get => (float)Math.Sqrt(x*x + y*y); 
    }

    public Vec2(int x = 0, int y = 0){
        this.x = x; this.y = y;
    }

    public override string ToString() 
        => $"({this.x},{this.y})";

    public int CompareTo(object? v){
        
        Vec2 vector = v as Vec2;
        
        float diff = (this.Magnitude - vector.Magnitude);
        return (int)(diff/diff);
    }

    public bool Equals(Vec2? v){
        return this.x = v.x && this.y == v.y; 
    }
}

...
var vecs = List<Vec2>(); // populated
vecs.Sort(); // will sort based on CompareTo()
```

### `.SequenceEqual()`

```C#
var vecs = new List<Vec2>{
    new Vec2(6,8),
    new Vec2(3,4),
};

var vecs2 = new List<Vec2>{
    new Vec2(6,8),
    new Vec2(3,4),
};

bool res = vecs.SequenceEqual(vecs2); // true
```

> `.SequenceEqual()` compares element by element (in order) using the `.Equals()` to compare equality between object. So if you `.Sort()` one of them it would return **`false`**


### `.Except()`

```C#
Item[] items = {
    new Item("Yakult", 5f),
    new Item("Milk 2L", 15f),
    new Item("Milk 3L", 20f),
    new Item("Tonkatsu", 5f)
};

Item[] milks = items.Where(item => item.Name.StartsWith("Milk")).ToArray();

foreach(Item i in items.Except(milks)) 
    Console.WriteLine(i);
```
Output
```
Yakult: $5
Tonkatsu: $5
```

> `Intersect()`, `Concat()` and `Union()` also can be used the same way

<br>

### `.Join()`
```C#
var query = from person in people
join pet in pets on person equals pet.Owner
select new{
    OwnerName = person.Name
    PetName = pet.Name
}

foreach(var pair in query)
    Console.WriteLine($"{pair.PetName} is owned by {pair.OwnerName}");

```

## Aggregate

- `.Count()` - self explanatory
```C#
var res = items.Where(item => item.Name.StartsWith("Milk")).Count();
```
- `.Min()` and `.Max()` - works as long as the elements implement `IComparable<T>.`

> I am so confused with .Aggregate()

## LINQ Executions
### Deferred Execution
A Query is a data structure ready to execute. It is not executed until a value is needed. The execution happens during **`foreach()`**, `Count()`, `ToList()`, `OrderBy()`, etc.

```C#
var query = list.Where(item => item.Color == "Red");

foreach(var i in query) // query is executed here
    Console.WriteLine(item);
```

### Immediate Execution
Query is executed immediately. 
```C#
var query = list.Where(item => item.Color == "Red").ToList();
```


