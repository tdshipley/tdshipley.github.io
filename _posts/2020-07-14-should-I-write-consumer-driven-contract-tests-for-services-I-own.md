---
title: Should I Write Consumer-Driven Contract Tests for Services I Own?
date: 2020-07-14T12:31:32+01:00
author: Thomas
layout: post
categories:
  - pact
  - consumer driven contract testing
tags:
  - pact
  - consumer driven contract testing
---

The [Ministry of Testing Slack Channel](https://www.ministryoftesting.com/slack_invite) is free to join and a great place to ask questions of the testing community. A (paraphrased) question I was asked recently:

> If I own two services which integrate - do I need to set up a consumer-driven (pact) contract test between them? Perhaps I can use a simple integration test instead?

It is a question I have come across a few times now when working with teams. 

## TL;DR; Yes you Should

Just because you own both services doesn’t mean the relationship between them stops existing. A Consumer-Driven Contract Test will allow you to keep tabs on that relationship and catch any drift between the two services without expensive, slow and hard to maintain integration tests.

## A Quick Recap - What is a Consumer-Driven Contract Test (CDCT)?

I have written before about [what a CDCT is](https://tomdriven.dev/.net%20core/c%23/contract%20testing/pact/test/2018/03/13/contract-testing-with-pact-in-net-core.html) but as a quick recap. A CDCT is a contract test where your consumer defines the API contract. The inverse is a more typical contract test relying on the API provider (developer) to define the contract.

It is preferable to have the consumer define the contract. The resultant contract will more accurately reflect API usage and is less likely to go out of date as the contract is generated by the consumer’s test suite.

I like to use [Pact](https://pact.io/) as a framework to write these tests but there are other options like [Postman](https://saucelabs.com/blog/intro-to-contract-testing-getting-started-with-postman).

So that is what a CDCT is. But what is the purpose?

### Testing Relationships - The Key to a Successful System

Whether we use integration, end to end or CDCT techniques they are all aiming to do the same thing - test relationships. When we write and execute these tests teams and individuals say things like:


> We are checking the system *hangs together*.

What is meant by the phrase *hangs together* is the system communicates well together. The Basket service can *speak* to the Payments service. The Authorisation service *verifies* that only certain users in the Accounts service can access a resource.

These are relationships and they are critical, without them, you don’t have a system. This is more prevalent in a microservice architecture where the number of relationships increases.

## So Back to the Question. Why Integration Tests Can’t Replace CDCTs?

The original question comes in two parts:

### Do I need to use a CDCT if I own both services?

**Yes**

The relationship between your two services still exists when you own the development of them both. The question hints that maybe because both sides of the relationship are owned by the same team that the contract between both services will be easily be maintained - this is not my personal experience.

Imagine a team that owns multiple small well-designed services that all communicate with each other. Like all teams, you are subject to changing requirements and priorities. You spend some time working on one service and then switch to the next. In this scenario, it is very easy for the relationship between just two services to drift.

You or a colleague makes a change in one service which changes to the format of an attribute importantly - let’s say a date field (they are tedious…) well that is easily missed - it is subtle. If you had a CDCT this would be picked up immediately. With an integration test, it *might* be picked up if you designed the test to check that.

### Can an Integration Test Replace a CDCT?

**No**

Integration tests can test relationships and CDCTs are not suitable all the time. For example, an external service which will not work on creating CDCTs with you. But in most cases, integration tests are a poor choice for testing relationships - because they are...

#### Slow

Either because they are waiting for an environment to be spun up or some other downstream system. A CDCT doesn’t wait for any system. It is a decoupled approach to relationship testing meaning you get faster feedback and don’t need to maintain an integration testing environment.

#### Brittle

The previous example of a date change shows how brittle an integration test can be. Unless your integration test had a specific assert of the date format the issue won’t be picked up. Now I can imagine you saying:

> A well-designed integration test will have a format check.

Maybe. But maybe it just checks the date can be *parsed* rather than a specific format? A CDCT will pick up the format change even if you didn’t specifically write an assert for it (unless you decided to accept any string… then it is on you!).

Integration tests also rely on a specific environment. Either a long-running or temporarily generated environment which inevitably breaks over time (OS & Package updates, config changes) so has to be maintained. CDCT don’t require this. Instead sharing a contract file to support decoupling.

## Consumer-Driven Contract Tests > Integration Tests

Integration tests have their place. Sometimes it will be impractical to set up a CDCT because you haven’t got the required cooperation.

But in most cases, I would recommend using a CDCT over an integration test. This advice doesn’t change if you own both sides of the relationship. The same issues as before exist. If anything it makes it easier for you to adopt CDCTs as you don’t need to convince another team!