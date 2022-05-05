# .NET

.NET is an open source **developer platform** for building different types of apps.

> **developer platform** - the languages & libraries that you use; together is a developer platform

**Languages**: C#, VB, F# <br>
**Platforms**:
- **.NET Core:** (runs anywhere) Windows, Linux, macOS
- **.NET Framework**: websites, services, and apps on Windows
- **Xamarin/Mono**: .NET for mobile
- **.NET standard** the shared set of libraries for all of the above

## Dependencies
- dotnet-host 6.0.2.sdk102-1
- dotnet-runtime 6.0.2.sdk102-1
- dotnet-sdk 6.0.2.sdk102-1
- dotnet-targeting-pack 6.0.2.sdk102-1

## Hello World
[Microsoft - Hello World](https://dotnet.microsoft.com/en-us/learn/dotnet/hello-world-tutorial/intro)<br>
Run this in the terminal to create an app: and cd to it
```bash
~$ dotnet new console -o MyConsoleApp -f 6.0
~$ cd MyConsoleApp
```

> Explanation:
> - `dotnet new console` creates a new **console** app
> - `-o` parameter creates a new directory called *MyConsoleApp* where your app will be stored
> - `-f` parameter indicates you're using .NET6 application

To run your app:
```bash
~$ dotnet run
Hello World!
```



---
### Resources:
- [Youtube - .NET for beginners (playlist)](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oWoazjhXQzBKMrFuArxpW80)
