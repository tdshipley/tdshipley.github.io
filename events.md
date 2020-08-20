---
layout: page
title: Events
permalink: /events/
---

Upcoming and previous dates are listed below with links to the slides. References are included on a final slide which isn't covered at the event.

## Verifying Relationships: Consumer-Driven Contract Tests and Microservices

### Dates

| Event                                                             | Date       |                                                                       |
| ----------------------------------------------------------------- | ---------- |-----------------------------------------------------------------------|
| [London Tester Gathering](http://bit.ly/3955bXU)                  | 25/02/2020 | [Slides](http://bit.ly/2TmIgAq)                                       |
| [Ministry of Testing Buckinghamshire](https://bit.ly/32i7wht)     | 06/08/2020 | [Slides](https://bit.ly/31qeLC7), [Recording](https://bit.ly/3kzGZCZ) |
| [TAQfull](https://bit.ly/2B21CWA)                                 | 13/08/2020 | [Slides](https://bit.ly/31RB4Ay), [Recording](https://bit.ly/3hhOlZK) |
| [CTM: Continuous Testing Meetup London](https://bit.ly/3a16Oam)   | 20/08/2020 | [Slides](https://bit.ly/2QcXY08)                                      |
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
