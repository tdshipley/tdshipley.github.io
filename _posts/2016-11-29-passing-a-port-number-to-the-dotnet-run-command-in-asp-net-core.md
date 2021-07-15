---
title: Specifying a Port Number to the dotnet run Command in ASP.Net Core
date: 2016-11-29T16:46:19+00:00

layout: single
categories:
  - .NET Core
---
ASP.Net core lets you run a web server for your web application from the command line with the command:

`dotnet run`

But there is no command argument passing the port to listen on. For example in Ruby on Rails you could specify the port with the _-port (-p) _argument:

`rails server --port 2000`

Instead, ASP.Net Core uses the environment variable _ASPNETCORE_URLS_ to take a string representation of the port and hostname of the server. If you want to change the port that the server listens on at the command line you will need to set the environment variable. Which you can do within the scope of the command:

```
# Unix:
ASPNETCORE_URLS="https://*:5123" dotnet run

# Windows PowerShell:
$env:ASPNETCORE_URLS="https://*:5123" ; dotnet run

# Windows CMD (note: no quotes):
SET ASPNETCORE_URLS=https://*:5123 && dotnet run
```

It would be nice if ASP.NET Core supported this in a similar way to rails but it seems the team has taken a different approach to configuration - relying on environment variables. It's the same [if you need to specify the environment too.](http://andrewlock.net/how-to-set-the-hosting-environment-in-asp-net-core/)