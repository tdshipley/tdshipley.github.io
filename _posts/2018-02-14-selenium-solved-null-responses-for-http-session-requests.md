---
title: 'Selenium Solved: Null Responses for HTTP Session Requests'
date: 2018-02-14T09:00:59+00:00
author: Thomas
layout: single
categories:
  - .NET Core
  - asp.net core
  - 'C#'
  - Selenium
---
Recently I was updating the UI tests in a project now Selenium Webdriver plays nice with .NET Core. And came across a strange error:

```
OpenQA.Selenium.WebDriverException : A exception with a null response was thrown sending an HTTP request
to the remote WebDriver server for URL http://localhost:51027/session/71f17e73965ce00cdd20434b035cdce2/element
```

What made this a strange error is it is a failure to communicate with the **Webdriver Server**, not my underlying application and because of this failure in communication Webdriver could not manipulate my website.

# The Fix

After some googling, this turns out to be a straightforward fix - my project uses the Chromedriver server as it's Webdriver for tests and simply the Chromedriver server executable I had locally was out of date when compared to my installed version of Chrome. So the fix was to [download the latest version](http://chromedriver.storage.googleapis.com/index.html).

## Manually Managing Chromedriver

I wouldn't have come across this error if I chose to include a Nuget package to download the latest version of Chromedriver for me and in a lot of scenarios, this is the sensible choice but what I like about managing the file myself is it isn't going to be updated accidentally by Nuget somehow - it is pinned hard at its current version and without my intervention that won't change. But given the error above and how long it might have taken to figure out&#8230; perhaps I should reconsider!