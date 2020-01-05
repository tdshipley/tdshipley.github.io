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

https://gist.github.com/tdshipley/35c2fc7a12ff59eb216a8d4268a383c4

# The Fix

Turns out this is a simple issue to fix. Just make sure that in the _Configure() _method in the _Startup_ class contains a call to _app.UseAuthentication()_ before the call to _app.UseMvc()_ for example:

https://gist.github.com/tdshipley/fcee610744e51fed2dc11eef379caebf

With this method updated to include the Authentication middleware, the issue should be resolved.





