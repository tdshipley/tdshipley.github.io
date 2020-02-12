---
title: QA Interview Tip: Everything is Not Awesome
date: 2020-02-12T10:18:32+01:00
author: Thomas
layout: post
categories:
  - interviewing
tags:
  - interviews
---
## Lego Got It Wrong and That is OK

Everything is _not_ awesome (despite the catchy [song](https://www.youtube.com/watch?v=9cQgQIMlwWw)) and you don't like every QA tool or technology you have ever worked with and neither do I, at least not completely.

__And that is ok.__ I am not going to judge you in an interview for saying you don't like a certain tool, tech or technique either partially or completely. In fact, as an interviewer, I often ask interviewees what QA thing they don't like. I am suspicious when they say nothing (unless you are inexperienced). It is important to question the body of knowledge we have as a community and to constantly evaluate it.

Without questioning what we are doing and why we all risk becoming cargo cult QAs. I want to work with people who are looking for the best way of doing things and not because that is how they have always been done.

### A Caveat... Tell Me Why

Please if you don't like something then tell me why. Just saying I dislike BDD or Generic Unit Test Framework with no follow up doesn't show me your critical thinking skills. If you don't like something say why you don't. It might be buggy, it could be lazily implemented or perhaps it gets in your way.

## Things I Don't Like in QA

In the spirit of this post here are some things I don't like in the QA world. If you are ever in an interview with me feel free to ask about them. They are all concepts rather than technology for no particular reason.

### The Test Pyramid

Simplistic, misused and rarely implemented correctly. The key idea behind the Test Pyramid in fairness is a good one - let’s have most of our tests as tightly scoped as possible. So instead of lots of end to end tests, we have lots of little focused ones instead.

The problem, however, is the pyramid is often supported dogmatically in my experience and rarely implemented well. Instead, teams often try to build up testing in the layers of pyramid rather than thinking about risk what is the highest priority. This, in the end, makes teams feel bad that they never hit the mythical perfect pyramid shape.

#### Read More

* [Testing is Good. Pyramids are Bad. Ice Cream Cones are the Worst](https://medium.com/@fistsOfReason/testing-is-good-pyramids-are-bad-ice-cream-cones-are-the-worst-ad94b9b2f05f)

### Integration Tests

I can see the appeal of Integration Tests. Your system is made up of many moving parts and you want to check that they work together. But you don't want to set up the whole system as it would take too long and is too expensive so you do it in chunks.

The problem with this is the testing in chunks is still expensive and takes too long. Orchestrating your chunks together on an environment can be painful. Setting up test data which avoids conflicts between tests can be worse.

If your system is made up of many services then I prefer _consumer driven contract tests_ with only a __very small__ amount of integration/end to end tests. The small amount of integration/end to end tests that are left act as a sanity check of the very basics of your system. The consumer-driven contract tests verify all the little relationships between the different parts.

#### Read More

* [Just Say No to More End-to-End Tests](https://testing.googleblog.com/2015/04/just-say-no-to-more-end-to-end-tests.html)
* [Integrated Tests Are A Scam](https://blog.thecodewhisperer.com/permalink/integrated-tests-are-a-scam)
* [Consumer Driven Contracts: A Service Evolution Pattern](https://martinfowler.com/articles/consumerDrivenContracts.html)
* [Pact.io](https://pact.io/)


### BDD Everywhere

You have a suite of Integration or End to End tests and they are written with Selenium. Having read some testing blogs you now use a BDD framework on top like Cucumber because it allows developers and business people alike to read tests in English like language. If your team actually does read the cucumber specs to help with understanding then I don't have a problem with the technique.

A lot of places don't do that. They do BDD because someone told them they should. No one ever reads the scenarios when they are completed. It is just an extra layer of complexity in your test framework.

Worse still the scenarios which are meant to be readable by anyone are poorly written. I have seen versions of the below _many_ times:

```
Given I visit www.google.com
And I check that the 'Search' button is on the page
And I check that the 'Feeling Lucky' button is on the page
And I check the Google Logo is on the page
And I enter the search term 'BDD is fun'
And I click the 'Search Button'
Then I see the Search results page
And The page has results
And they are clickable
```
That is a mild example (because I got bored) - I have seen many that are much worse.

#### Read More

* [Why I recommend against using Cucumber](https://www.codewithjason.com/recommend-against-cucumber/)

## Be Honest and Critical
You are in an interview to show someone two main things - that you are [Smart and Get Things Done](https://www.joelonsoftware.com/2006/10/25/the-guerrilla-guide-to-interviewing-version-30/). (I know there are other skills to display as well...)

Being _Honest and Critical_ about testing trends and tools shows me you are smart. It potentially shows me that you want to get things done too by avoiding doing things for the sake of doing them.