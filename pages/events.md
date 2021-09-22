---
permalink: /events/
layout: single
classes: wide
title: Events
---

Upcoming and previous dates are listed below with links to the slides. References are included on a final slide which isn't covered at the event.

## Creating Test Strategies Teams Will Read

### Dates

| Event                                                             | Date       |                                                                       |
| ----------------------------------------------------------------- | ---------- |-----------------------------------------------------------------------|
| [Ministry of Testing](https://bit.ly/3BxNq16)                     | 21/09/2021 | [Slides](https://bit.ly/3AxFxIU)                                      |

### Details

Test Strategy is an overloaded term. Some fear multiple pages of formal documents that no one will read. Others want every detail documented formally and tightly version controlled. What is best? More importantly, what is best for your project? The context is the key.

This session dives into the detail of test strategies. Discussing what works well for different project contexts, common strategy types, and how to get your team to read it.

#### Outcomes

* Appreciate the importance of a test strategy.
* Understand what type of strategy style is best for a project.
* Increase team engagement with a test strategy.

## Ready for Test - a Symptom of a Poor Quality Culture

### Dates

| Event                                                             | Date       |                                                                       |
| ----------------------------------------------------------------- | ---------- |-----------------------------------------------------------------------|
| [CTM: Continuous Testing Meetup London](https://bit.ly/3kn0pO1)   | 30/06/2021 | [Slides](https://bit.ly/3B1wFMw), [Recording](https://bit.ly/3iyHInE) |
| [2nd. Test Busters Day & Night](https://bit.ly/3Bu7elU)           | 09/09/2021 | [Slides](https://bit.ly/3u2U9NX)                                      |

### Details

The Ready for Test column on our boards feels safe, doesn’t it? A well-known column with a clear purpose, at least that is how it might seem. But what if this column is doing more harm than good in your team?

Ideas such as Shift Left and Continuous Integration are increasingly popular. This popularity stems from early feedback, sharing knowledge and ownership between team members. Yet Agile software teams continue to treat QA concerns as a separate stage owned by different people. QA team members provide feedback after the task, hoarding knowledge and being passed the ownership of quality.

In this talk, I want to convince you that in many cases, Ready for Test, In QA and other quality gate columns do more harm than good. They contribute to a culture of separation between QAs and other team members. This separation causes quality to decrease. There is a better way.

## Verifying Relationships: Consumer-Driven Contract Tests and Microservices

### Dates

| Event                                                             | Date       |                                                                       |
| ----------------------------------------------------------------- | ---------- |-----------------------------------------------------------------------|
| [London Tester Gathering](http://bit.ly/3955bXU)                  | 25/02/2020 | [Slides](http://bit.ly/2TmIgAq)                                       |
| [Ministry of Testing Buckinghamshire](https://bit.ly/32i7wht)     | 06/08/2020 | [Slides](https://bit.ly/31qeLC7), [Recording](https://bit.ly/3kzGZCZ) |
| [TAQfull](https://bit.ly/2B21CWA)                                 | 13/08/2020 | [Slides](https://bit.ly/31RB4Ay), [Recording](https://bit.ly/3hhOlZK) |
| [CTM: Continuous Testing Meetup London](https://bit.ly/3a16Oam)   | 20/08/2020 | [Slides](https://bit.ly/2QcXY08), [Recording](https://bit.ly/3aRttGz) |
| [Nordic Testing Days 2021](http://bit.ly/32wn3rY)                 | 04/06/2021 |                                                                       |

### Details

Microservice architecture brings many benefits but there is one potential pitfall when testing them.
How do you model and test the many relationships between services? You could try integration tests but they are expensive to maintain,
slow to run and come with orchestration complications.

Contract testing could help with this. But the traditional contract test has a circular problem.
The team writing the service defines the contract and the test.
As soon as this isn’t kept up to date (only a matter of time) the test is useless.

A better approach is Consumer-Driven Contract testing. Here we use the output of contract tests owned by your consumers to test your API.
This talk will introduce you to the Pact framework to write these tests and the key concepts.
You will be able to avoid that integration test pack and have more time for other test activities in your team.

![Speaking at London Tester Gathering](/assets/img/events/verify_relationships.jpg)
