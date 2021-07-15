---
title: Going Beyond Test Coverage
date: 2021-03-11T15:31:32+01:00
author: Thomas
layout: single
categories:
  - automated-test
tags:
  - metrics
  - automated tests
---

Why are you writing automated tests for your project? I hope the answer is to find defects!
Writing tests is not free - someone somewhere must design, develop and maintain them.
All of this is expensive so we must get something out of our investment.

So how are you proving that your automated tests are valuable and what is the value they deliver?

## What is Value? Automated Tests that Always Pass or Fail?

> Automated tests are at there most valuable when they catch defects/bugs.

What value do tests that always pass or fail generate? Probably not much - perhaps they even
detract! In my experience, the tests slowly become ignored noise due to a constant pass/fail state which
will either be attributed to a 'flakiness' or a 'reliable' feature. Who knows if that is the case.

If your automated tests always pass or fail it is time to review them. An automated test suite that doesn't catch
any defects isn't useful. Nor is a test suite that cries wolf all the time. There are multiple reasons why this could be
the case perhaps the test suite isn't rigorous enough or asks the wrong questions.

## Test Coverage - a Poor Metric for Value

> Test coverage doesn't prove you have valuable tests.

If we agree that valuable tests are those that find defects then tracking test
coverage doesn't tell us anything about value. Test coverage doesn't tell us if a test catches defects. 
If I have a project with 100% test coverage does that mean I have a valuable test pack?

We cannot answer this question. We need to dig deeper.

## Going Beyond Test Coverage

So if Test Coverage is a poor metric what metrics work well for discovering value?
There are many you could use - I have picked out a few I like.

To implement these metrics you will probably need to combine some manual effort
with automated reporting. But the results are worth it. You will start to see how valuable your tests are.

### Metric 1: False Negative Rate

> If you cannot fix a test you must remove it!

Flakiness, flapping tests, unreliable tests - most test suites have them. Tests
which for whatever reason sometimes fail. It could be down to multiple things; environment, poor design,
strict assertions or a timing issue.

Tracking these failures is very important. You want to see which tests have a high false-negative rate
because these tests are detracting value from your suite. They are noise. Once you identify these tests
you have two options. Fix or remove them.

Some objections to removal I have come across:

#### Tests an Important Feature

_The unreliable test is important - we need it to test feature X._

An inconsistent test cannot be relied upon. If the test fails do you have confidence in that failure?
Does your team? It is much better to remove or redesign the test.

Inconsistent tests will eventually be ignored by the team. You do not want that.

#### Test Coverage will Drop

Again test coverage doesn't tell us anything about value. Test coverage is not as important as valuable
working tests are.

### Metric 2: False Positive Rate

> It is better to have a test suite that has failures in its execution than a 100% pass rate.

Worse than an unreliable test is a test that always passes so potentially missing defects. Every time
you raise a defect ask the question should the automated tests have caught this? If the answer is yes
and the test exists then note it down. Start to track how many times a test misses a defect.

If you have tests that are consistently missing defects you have a problem. Again you should redesign
or remove that test. It is giving your team false confidence.

### Metric 3: Execution Time

> Slow test suite execution slows your team down and detracts value.

How long do your tests take to run? A test suite is most valuable when it provides fast feedback.
This allows the team to quickly check work and act on the results. If your team has to wait for an
overnight run of tests before release they will be slowed down. When a 
test suite slows down a team in this way it starts to detract value.

If you see your execution time creeping up then start to think about how you can bring it down. Hopefully,
your tests are designed so they can be executed in any order without issues. If that is the case
perhaps you could execute tests in parallel?

### Metric 4: Confirmed Defects Raised

> Tests that find defects are creating value.

This is a simple but powerful metric. Start to record how many defects a test has found. But not just count
also record impact and criticality. Start to get a sense of how valuable the defects your tests find are.
Use this to demonstrate the value or lack of your test suite brings to the project.

### Metric 5: Defect Clustering

> Defects often occur in clusters. Tracking these clusters will help you plan your tests.

Every tester has come across defect clustering even if they don't realise it. Have you
ever been working on something and have a gut feeling, this feature always breaks?
That is defect clustering at work. Where you find a defect you will often find others and they
can be described as a cluster.

Break your project into clusters. This could be done by feature or perhaps repository. Each time a 
defect is found by your test suite track what cluster it was found in. Start to see where the pattern forms.
Use this to guide where you invest your time in a test suite.

Perhaps the Shopping Cart seems to always have issues but after tracking defects in clusters you find it is the
Payment logic is the issue. Tracking this way goes one step beyond gut feel.
You can prove that the tests you are planning to write will be valuable because you are using data to target troublesome
areas of your application.

## Writing Tests and Tracking Coverage is Not Enough

It is not enough to just write lots of tests that increase your test coverage metric.
We can do better by focusing on tests that find defects. Finding defects is what we want from our test suites after all!

Tracking defects found, the impact of those defects and where they appear you can start to plan tests based on
data and provide more value to your team.