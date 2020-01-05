---
title: Setting Up SQLite and Entity Framework Core in ASP.Net Core
date: 2016-03-24T13:40:33+00:00
author: Thomas
layout: post
categories:
  - .NET Core
  - 'C#'
  - Entity Framework
---
For small applications such as prototypes and small side projects, [SQLite](https://www.sqlite.org/whentouse.html) is a great choice for a relational database. It is really easy to setup because:

  * Its self-contained 
      * Its just one database file in your project.
  * No server 
      * Because its just one database file in your project which holds all your data there is no extra server setup.
  * No configuration 
      * All you need is to create your schema and the database is ready to store data.

## Letting Entity Framework Core Manage Your Database Schema

For all its ease to setup, you still need a schema to define your tables and the relationships between them. Unless your a SQL expert this goes against being able to quickly spin up and database for your ASP.Net Core application - which is one of the main reasons to use SQLite! But its really easy to setup [Entity Framework Core](https://github.com/aspnet/EntityFramework) to do this for you.

### Updating the project.json File to Gather the Needed Dependencies

The first step is to update your project.json dependencies to get some nuget packages that will be used. These are:

  * _[EntityFramework.Sqlite](https://www.nuget.org/packages/EntityFramework.SQLite/)_ 
      * The code EF will use to connect to SQLite
  * _[EntityFramework.Commands](https://www.nuget.org/packages/EntityFramework.Commands/7.0.0-rc1-final)_ 
      * The common EF commands. For example, running and creating migrations.
  * _[Microsoft.Extensions.PlatformAbstractions](https://www.nuget.org/packages/Microsoft.Extensions.PlatformAbstractions/1.0.0-rc1-final)_ 
      * Only needed if you plan to compile your code on non-windows platforms (_in my case a Mac_)

#### Add an EF command to the Commands Object

If you haven't already ensured you have an _ef _command listed in your commands object - this is used when running entity framework commands via a command prompt.

https://gist.github.com/tdshipley/85868bb2b332ef2316e5

### Create Models to Represent Tables in the Database

This isn't specific to using SQLite with EF. But for the sake of completeness create a model class for each table that will be in the database. The [EF Core Documentation has an example.](http://ef.readthedocs.org/en/latest/platforms/coreclr/getting-started-osx.html#create-your-model)

### Create a DBContext for your Database

Again this isn't specific but creates a DBContext which represents the properties and relationships of the tables in the database. Again the [EF Core Documentation has an example.](http://ef.readthedocs.org/en/latest/platforms/coreclr/getting-started-osx.html#create-your-model)

### Add Entity Framework to the Application in ConfigureServices in Startup.cs

The final part of the setup is to let ASP.NET core know you want to use EF Core with SQLite you can do this by adding it as a service to ConfigureServices in Startup.cs with your context passed in as a generic type:

https://gist.github.com/tdshipley/2a5f80a4b375864578df

The code is conceptually straightforward it defines where the SQLite database file is on the file system and passes that information to EF when it is added to the services the ASP.NET application consumes.

#### PlatformServices only Needed When Compiling outside Windows

In this example, it uses PlatformServices to get the application base path as the code is being written to compile using .NET Core on OSX and Windows. Otherwise, use:

```csharp
System.Environment.CurrentDirectory
```

### Create and Run an Initial Migration

To create a migration in the command line type:

```bash
dnx ef migrations add Initial
```

Where _Initial _is the name of your migration. Once the migration has been created you can run your migration by typing:

```bash
dnx ef database update
```

## Summary

If all has gone well you will now have an SQLite database managed by EF Core which means you can handle or future changes by updating your models / DB Context and using migrations to apply them to the database in a similar way to how the Initial migration was created.