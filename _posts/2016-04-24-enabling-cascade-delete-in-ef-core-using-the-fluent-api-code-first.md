---
title: Enabling Cascade Delete in EF Core Code First DB Using the Fluent API
date: 2016-04-24T19:50:02+01:00
author: Thomas
layout: post
categories:
  - .NET Core
  - 'C#'
  - Entity Framework
---
## Entity Framework Core Default Behaviour on Delete

Cascade delete saves a developer time by not needing to write boilerplate code for related data when the parent data in the relationship has been deleted. However in Entity Framework Core it is not the default behaviour. It takes a more conservative view and sets the on delete behaviour to _restrict_ ([StackOverflow Question where EF Core Team Member Confirms](https://stackoverflow.com/questions/36010867/entity-framework-parent-child-linking-and-foreign-key-constrain-failed-error))_ _which the documentation defines as:

> **Restrict:** The delete operation is not applied to dependent entities. The dependent entities remain unchanged. - [EF Core Documentation](https://docs.efproject.net/en/latest/modeling/relationships.html#id2)

Compared with the definition of cascade:

> **Cascade:** Dependent entities are also deleted. - [EF Core Documentation](https://docs.efproject.net/en/latest/modeling/relationships.html#id2)

## Enabling Cascade Delete Using The Fluent API

If you have created your database using Code First then the fix is simple. When defining your relationships tell EF that you want the delete action to be a cascade one. This needs the use of an additional using _Microsoft.Data.Entity.Metadata _which contains _DeleteBehaviour_:

https://gist.github.com/tdshipley/10e982fd9469d7cf76e0461bbd11177f