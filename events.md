---
layout: page
title: Events
permalink: /events/
---

Seen me speak at a meetup, conference or would like to?

Upcoming and previous dates are listed below with links to the slides. The slides have a references page at the end which isn't covered at the event.

## Verifying Relationships: Consumer-Driven Contract Tests and Microservices

### Dates

| Event                                              | Date       |                                  |
| -------------------------------------------------- | ---------- |----------------------------------|
| [London Tester Gathering](https://bit.ly/2VqyYpV)  | 25/02/2020 | [Slides](https://bit.ly/2Vqog2E) |
| [Nordic Testing Days 2020](https://bit.ly/2vcz0Ho) | 05/06/2020 |                                  |

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

![Speaking at London Tester Gathering](/assets/img/events/verify_relationships.jpg){:height="80%" width="80%" .center}
