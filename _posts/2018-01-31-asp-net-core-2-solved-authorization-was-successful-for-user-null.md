---
title: 'ASP.NET Core 2 Solved: Authorization was successful for user: (null).'
date: 2018-01-31T09:00:17+00:00
author: Thomas
layout: post
categories:
  - .NET Core
  - asp.net core
  - 'C#'
---
While I was migrating an ASP.NET Core 1 project to version 2 my authentication code stopped working. After some investigation I kept running across this info message in my application logs which seemed unusual:

```
info: Microsoft.AspNetCore.Authorization.DefaultAuthorizationService[1]
Authorization was successful for user: (null).
```

# The Fix

Turns out this is a simple issue to fix. Just make sure that in the _Configure() _method in the _Startup_ class contains a call to _app.UseAuthentication()_ before the call to _app.UseMvc()_ for example:

```csharp
// This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
{
    loggerFactory.AddConsole(Configuration.GetSection("Logging"));
    loggerFactory.AddDebug();

    app.UseStaticFiles();
    app.UseAuthentication();
    app.UseMvc();
}
```

With this method updated to include the Authentication middleware, the issue should be resolved.





