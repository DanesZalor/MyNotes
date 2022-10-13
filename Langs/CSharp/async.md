# Asynchronous programming

```C#

static void Main(string[] args){
    Console.WriteLine("Start");

    Task[] tasks = new Task[2]{
        DelayedOutput("Hello", 2000),
        DelayedOutput("World", 1000),
    };

    Task.WaitAll(tasks);
    Console.WriteLine("End");
}

public static async Task DelayedOutput(string output, int delay){
    await Task.Run(() => {
        Thread.Sleep(delay);
        Console.WriteLine(output);
    });
}
```
#### outputs
```
Start
World
Hello
End
```

This line executes all tasks asynchronously and only moves on till all threads are done.
```C++
Task.WaitAll(tasks);
```

You can use `WaitAny()` which will stop once a single Task is finished.
```C++
Task.WaitAny(tasks);
```