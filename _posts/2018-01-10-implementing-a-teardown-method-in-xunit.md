---
title: Implementing a Teardown Method in XUnit
date: 2018-01-10T16:14:38+00:00
author: Thomas
layout: post
categories:
  - .NET Core
  - 'C#'
  - Test
  - xunit
---
[XUnit](https://xunit.github.io/) is a free open source unit testing tool for .NET written by the original inventor of NUnit v2 which is great to work with and supports .NET Core, however, how it handles clean up is slightly different to other test frameworks you may have used.

## What is a TearDown Method?

If you haven't done much-automated testing before then you may not know what a TearDown method is. Typically its the method responsible for cleaning up after your test(s) have run. For example, an integration test might create data which is persisted to a database. Afterwards, this needs to be purged of data in case the test failed and couldn't delete the data itself. In this scenario, it would be important that the data is deleted even when the test fails to ensure a consistent state for the start of each test.

## XUnit Doesn't Have TearDown Methods

However, compared to NUnit v2 it is missing a _TearDown_ attribute as highlighted in the [comparison table to other frameworks](https://xunit.github.io/docs/comparisons.html) as an alternative they suggest implementing the IDisposable interface.

### TearDown Methods Considered Harmful

XUnit doesn't include a TearDown attribute to create TearDown methods because the creator [believes they are bad](http://jamesnewkirk.typepad.com/posts/2007/09/why-you-should-.html). The reasons can be roughly summarised. Having a TearDown (and potentially a Setup) method impedes readability of tests as you need to look in up to three methods to know what a test method is doing:

_(Credit: http://jamesnewkirk.typepad.com/posts/2007/09/why-you-should-.html)_

```csharp
[TestFixture]
public class MyTests
{
    [SetUp]
    public void BeforeTest()
    {
      Console.WriteLine("BeforeTest");
    }

    [TearDown]
    public void AfterTest()
    {
        Console.WriteLine("AfterTest");
    }

    [Test]
    public void Test1()
    {
        Console.WriteLine("Test1");
    }

    [Test]
    public void Test2()
    {
        Console.WriteLine("Test2");
    }
}
```

I agree that Setup and TearDown are a bad idea when used for reducing code duplication between tests. There have been many times on a project where I personally have had to dig around multiple files because the actual definition of the test is scattered across them. It is much easier to duplicate things like console outputs and creating objects to test against. A good rule might be:

> Use _Setup_ and _TearDown_ methods to remedy side affects of tests **_not_** extract common behaviour.

So if you are cleaning up your database after some integration test which failed before it could do the clean up that's fine. However, if you are creating some objects that all your tests use then perhaps reconsider.

## Implementing IDisposable to Handle TearDown in XUnit Tests

Following the rule above it is clear that in some cases your tests will still need to clean up after themselves. Instead of a TearDown method, XUnit wants you to use the .NET Framework to handle your clean up code instead. This is a good thing you and developers in your team will probably be more familiar (or at least spend more time) with the .NET Framework than XUnit.

So, in the end, the solution is pretty simple - in your test class just implement IDisposable and in your dispose method do any cleanup work that you need to do:

```csharp
public class TruthTests : IDisposable
{
    public TruthTests()
    {
    }

    public void Dispose()
    {
        //Do cleanup actions here
        //
        // e.g.
        // 
        // var database = new Database();
        // database.reset();
    }

    [Fact]
    public void TrueEqualsTrue()
    {
        Assert.Equal(true, true);
    }
    
    [Fact]
    public void TrueDoesNotEqualFalse()
    {
        Assert.NotEqual(true, false);
    }
}
```

By implementing the IDisposable interface above there is now a hook we can use - the _Dispose()_ method which can be used to clean up after every test. The [XUnit Documentation](https://xunit.github.io/docs/shared-context.html) has more examples for different scenarios.

## Further Reading

  1. [Shared Context - XUnit Documentation](https://xunit.github.io/docs/shared-context.html)
  2. [IDisposable Interface - MSDN Documentation](https://msdn.microsoft.com/en-us/library/system.idisposable(v=vs.110).aspx)

##