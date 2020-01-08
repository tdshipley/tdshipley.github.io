---
title: Ignoring Folders During Compilation in a ASP.NET Core RC2 Project
date: 2016-05-23T15:39:12+01:00
author: Thomas
layout: post
categories:
  - .NET Core
  - 'C#'
---
# ASP.NET Core RC2 - DNX is dead. Introducing the DotNet CLI

Until RC2 of ASP.NET Core, the responsibility for building a project was handled by [DNX](https://github.com/aspnet/dnx) which has now been retired. This has been replaced by the [.NET CLI](https://github.com/dotnet/cli). Part of the motivation for this is to have one tool fulfilling the roles of DNX, [DNU](https://github.com/aspnet/Home/wiki/DNX-utility) and [DNVM](https://github.com/aspnet/dnvm) to try to make things less confusing for developers when they set up their environments.

# Ignoring a Folder in .NET CLI Compilation

One of the quirks during the transition to the .NET CLI from DNX was my project failed to compile. This was due to a node package that didn't support .NET Core. Luckily the fix is straightforward - but perhaps a little hidden to someone unfamiliar. Within your _project.json _in the _buildOptions_ section a _compile_ object can be added with a property called _exclude._ This is a list of folders to be ignored when compiling the project.

```json
{
  "buildOptions": {
    "emitEntryPoint": true,
    "preserveCompilationContext": true,
    "compile": {
      "exclude": [ "node_modules" ]
    }
  },
  "tools": {
    "SomeToolsRemovedForBrevity": true
  },
  "frameworks": {
    "netcoreapp1.0": {
      "imports": [
        "dotnet5.6",
        "dnxcore50",
        "portable-net45+win8"
      ]
    }
  },
  "dependencies": {
    "SomeDependenciesRemovedForBrevity": true
  },
  "publishOptions": {
    "include": [
      "wwwroot",
      "node_modules",
      "**.user",
      "**.vspscc"
    ]
  },
  "scripts": {
    "prepublish": [ "some", "prepublish", "steps" ],
    "watch": [ "gulp watch" ]
  },
  "userSecretsId": "somescerets",
  "version": "1.0.1-*"
}
```

With this in place, the node_modules folder in the project is ignored and the code compiles successfully.

