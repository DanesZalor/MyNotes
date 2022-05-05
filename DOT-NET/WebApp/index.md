# ASP.NET - Hello world

For more info, checkout this [tutorial](https://dotnet.microsoft.com/en-us/learn/aspnet/hello-world-tutorial/intro).

Run this command on the terminal to create your Web App
```bash
~$ dotnet new webapp -o MyWebApp --no-https -f net6.0
```

> Explanation
> - `webapp` arguement specified to make a webapp **template**
> - `-o` parameter creates a new directory called *MyWebApp* where your web app will be stored
> - `--no-https` specifies not to enable https protocol
> - `-f` indicates to use net6.0

#### What were the files created
- `Program.cs` contains the app start up code and middleware configuration.
- `Pages` folder contains some example web pages for the app.
- `MyWebApp.csproj` defines the project settings such as `.NET SDK` version to target.
- `Properties/launchSettings.json` defines different profile settings for the local developement environment.

#### Run the app
run this command inside the WebApp directory
```bash
~$ dotnet watch
watch : Hot reload enabled. For a list of supported edits, see https://aka.ms/dotnet/hot-reload. Press "Ctrl + R" to restart.
watch : Building...
  Determining projects to restore...
  All projects are up-to-date for restore.
  MyWebApp -> /home/djdols/Projects/Coding/Tests/MyWebApp/bin/Debug/net6.0/MyWebApp.dll
watch : Started
info: Microsoft.Hosting.Lifetime[14]
      Now listening on: http://localhost:5172
info: Microsoft.Hosting.Lifetime[0]
      Application started. Press Ctrl+C to shut down.
info: Microsoft.Hosting.Lifetime[0]
      Hosting environment: Development
info: Microsoft.Hosting.Lifetime[0]
      Content root path: /home/djdols/Projects/Coding/Tests/MyWebApp/
```

The `dotnet watch` command will build and start the app, and then update the running app whenever you make code changes. 

As you can see from the output, it says `Now listening on: http://localhost:5172` which means we can access that address from our browser

![accessing the listening address](.imgs/browsersc.png)

## Hello World

edit `Pages/Index.cshtml` and replace the contents of the `<div>` tag withL

```html
<h1> Hello World </h1>
<p>The time on the server is @DateTime.Now</p>
```

now if we refresh the browser we'll see:
![Hello world in browser](.imgs/browsersc2.png)