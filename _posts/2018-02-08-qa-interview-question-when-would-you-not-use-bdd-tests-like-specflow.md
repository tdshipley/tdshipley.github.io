---
title: 'QA Interview Question: When Would You Not Use BDD Tests Like Specflow?'
date: 2018-02-08T16:52:59+00:00

layout: single
categories:
  - interview
  - qa
---
# The Question

> When would you not use BDD tests like Specflow?

This is a question I have often asked and been asked in interviews and it is a great one because it challenges the candidate to be critical of a practice which has a lot of a good press and isn't something the candidate is likely to have a prepared answer for. [Behavior Driven Development](https://en.wikipedia.org/wiki/Behavior-driven_development) tests using tools like [Specflow](http://specflow.org/) and [Cucumber](https://cucumber.io/) are a useful means to create tests but should the technique always be applied?

## Skills Assessed

  * Critical Analysis
  * Industry Awareness
  * Explaining Concepts
  * Peer-Driven Debate

# Answering the Question

Like most interview questions experience is really helpful when answering this one and if you have ever worked in an environment that uses BDD for tests then you should answer the question using an example that draws from that experience. If not the answers below might give you a starting point to frame your analysis.

## A Bad Answer

> _Having your tests written in a English like syntax is always useful._

This isn't a good answer for a couple of reasons firstly I cannot think of any technique or practice in software development which is universally useful all of the time. Developing great software is about tradeoffs and BDD is not always a smart tradeoff. For one thing, it takes extra time to write and maintain those tests as there is another layer of abstraction to be handled in your testing. Secondly, the answer isn't a well-developed analysis - why is an English like syntax in tests always useful? An interviewer is likely (and well-advised) to push on this to see what the candidate can come up with.

## An OK(ish) Answer

After pushing on the above bad answer a bit you might get an answer which looks more like this:

> _Having your tests written in an English like syntax is always useful. It provides living documentation that is often lacking in software development projects and enables non technical people such as Project Managers to be included in the ownership of tests._

This answer is really an expansion of the bad answer above but in the expansion, the candidate has shown some more in-depth knowledge of what BDD style tests are and the benefits of them (living documentation, and increased ownership of tests) and in doing so delivered on the _industry awareness_ assessment in the question. However, this answer still fails to address the tradeoff involved in writing BDD style tests and further it doesn't address whether the two benefits needed might actually be needed. Because of this, it doesn't satisfy the _critical_ _analysis__ _portion of the question.

## A Good Answer

So far the candidate has given us an answer which shows awareness of what BDD style tests are and some evidence of understanding around them but shown no analysis skills - a key skill for a QA Engineer. The analysis part of the answer comes when the candidate talks about the disadvantages as well:

> _Having your tests written in an English like syntax is often useful. It provides living documentation that is often lacking in software development projects and enables non technical people such as Project Managers to be included in the ownership of tests. However, there is a trade off with BBD style tests as it adds a layer of complexity to your test suite because of managing the translation of the English like syntax to code. If a project was perhaps a proof of concept peice where it is more important to deliver a working demo or if there isn't buy in from the non technical staff on the team (or only a few of them) I would consider not implementing BDD tests as the benefits of doing so might not outweigh the costs. In the end it is best to decide on a project by project basis. _

The answer above is good because it handles a couple of points:

  * The advantages and disadvantages of using BDD style tests.
  * Examples of when it might not be worth implementing them.
  * Acknowledges that the decision on whether to use BDD style tests depends on the project being tested.

By handling the above points the answer displays to the interviewer a good understanding of the concepts involved and a discussion of how and when they might be applied. In doing so they have met all the assessment criteria.

# Conclusion

One of the key takeaways from this question I think is to make your answers example driven (real-world ones are best) and when asked about when to apply or not apply a concept always think in terms of trade-offs - show the interviewer that you understand that different software projects are rarely the same and require different approaches based on the circumstance. Avoid a militant for or against position!