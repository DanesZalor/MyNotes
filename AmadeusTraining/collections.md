# Collections

group data together and is indexable `this[index]`

can be foreach'ed and has debugger integration where you can see the elements inside the list

arrays implement `IList` I think since iirc they have `.Sort()`

> CSV files are Comma Separated Values.

### using **using** keyword

```C#
using (StreamReader sr = new StreamReader(_path)){
    ...
    // sr accessible here
}
// sr is disposed
```

**`using`** is important sometimes like `StreamReader` because when a StreamReader is initialized with a file, the file is locked. And unlocked when it is disposed

> only reference type values can be null<br>
> for number types they are often 0 if null

### `List<T>`

can be resized unlike an Array, useful when the length of the list is unknown upon instantiation. Useful for memory management since Lists uses a pointer to the next element instead of adjacent memory blocks

> wait joke the thing about memory is from a LinkedList not a List

`List<T>` besides `.Add()` also has `.Insert(index, item)` which is cool

And also `.FindIndex(lambda)`
```C#
countries.FindIndex(x => x.Population < 2_000_000>);
```

> `.FindIndex(lambda)` loops through the elements and assign it to `x` and then check if `x.Population < 2_000_000` and return the first instance where it is true. Helpful if the list is sorted

<br>
 
### `Dictionary<TKey, TValue>`

List except the index is a **key** rather than an index

```C#
var dict = new Dictionary<string, Object>();

Object o1 = new Object();
Object o2 = new Object();

dict.Add("key1", o1);
dict.Add("key2", o2);

dict["key1"]; //returns o1
dict["key123"]; // throws Exception

dict.TryGetValue("MUS", out Country country);
```

> Dictionaries are *hash map*'ed btw so it's much faster to Insert items.

#### Dictionary Initializer
```C#
var dict = new Dict<string, int>{
    {"key1", 420},
    {"key2", 69}
};
```

> Since Dictionarys are **Hashed**, the keys are **unique** and you can't add the same key


```C#
var dict = new Dictionary<string, string> ();

dict.Add("key1", "val1");
dict.TryGetValue("key1", out string res); // returns true

Console.WriteLine(res); // val1

// or you can use .ContainsKey() 
```



# LINQ and Collections

query collections extracting just the stuff you want. It is READONLY

### `.RemoveAll(Predicate)`
instead of iterating over a collection when you want to remove an element, you can use this instead:
```C#
countries.RemoveAll(x => x.Name.Contains(','));
```

### `.OrderBy(Predicate)`
```C#
countries.OrderBy(x=>x.Name);
```

### `.Take(int)`
```C#
list.Take(5); // returns a slice of the first 5 
```

> countries - data source  which it queries from<br>

```C#
countries.Where(x=>!x.Name.Contains(',')); 
// returns all countries which names doesnt contain a ,
```

> btw all these LINQ functions return an Enumerable which can be **`foreach`**'ed

> If an enumerable is null, it will throw an exception if it is **`foreach`**'ed

```C#
var fc = countries.Where(x=>!x.Name.Contains(','));

// is same as

var fc = from c in countries 
where !c.Name.Contains(',') 
select c;

/* how ever linq query syntax does not support 
everything that linq methods can do such as .Take()
*/
```

## Jagged Array
  
an array or arrays. Except, it's not a multidimensional array (in C# that is called a matrix). In a jagged array, the array element inside the array doesn't have to be equal in length.

```C#
int[][] jagged = {
    new int[],
    new int[],
    new int[],
}

int[,] matrix = new int[3,3];
```

---

## Immutable collections
 
Collections but immutable (duh). USeful if you don't want the contents to ever change

|Standard|Immutable|
|-|-|
|Array|ImmutableArray|
|List|ImmutableList|
|Dictionary|ImmutableDictionary|

It's great for multithreaded apps to prevent race conditions

> All the standard generic collections are not thread safe, they are designed to be used for single thread<br>For multithreaded applications, use **`Concurrent Collections`** and **`Immutable Collections`** 

