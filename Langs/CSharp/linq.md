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