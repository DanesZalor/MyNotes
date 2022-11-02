### [Asynchronous Programming with `async` and `await`](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/async/#final-version)

Normally, computers execute a task sequentially. Meaning they have to finish one task before starting another.

But realistically, we want to do tasks asynchronously if our resources can handle it. 

Say we have a `Toaster` class that can **`async`** `ToastBread()` but has a limited `Bread` slots.

```C#
using System.Threading.Tasks;

class Bread{}
class Toast{}

class Toaster
{
    public const int SLOTS = 2;
    private int _takenSlots = 0;

    public async Task<Toast> ToastBread(Bread bread)
    {
        // check every second for extra slot
        while(_takenSlots >= SLOTS)
            await Task.Delay(1000);
        
        _takenSlots ++;

        Console.Write("Putting bread in the toaster\n");
        await Task.Delay(3000); // takes 3s to toast
        Console.Write("Removing toast form toaster\n");

        _takenSlots--;

        return new Toast();
    }
}

...
static async Task CookBreakfast()
{
    var toaster = new Toaster();
    
    await Task.WhenAll(new Task[]{
        toaster.ToastBread(new Bread()),
        toaster.ToastBread(new Bread()),
        toaster.ToastBread(new Bread())
    });
}

public static void Main()
{
    CookBreakfast.Wait();
    Console.Write("Finished cooking breakfast");
}
```

**`Output`**
```
Putting bread in the toaster // 1st bread
Putting bread in the toaster // 2nd bread
Removing toast form toaster  // 1st bread done
Removing toast form toaster  // 2nd bread done
Putting bread in the toaster // 3rd bread
Removing toast form toaster  // 3rd bread done
Finished cooking breakfast
```

asynchronous Tasks can be made from (but not limited to) functions with **`async`** keyword and `Task<T>` or `Task` return type. Then you can use the `Task` static class to manage the tasks such as the `Task.WhenAll(IEnumerable<Task>)` which is awaitable.