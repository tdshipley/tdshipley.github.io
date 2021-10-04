---
title: Test Strategy - Understanding Your Readers Goals
date: 2021-10-20T15:31:32+01:00

layout: single
categories:
  - test-strategy
tags:
  - leadership
  - test-strategy
  - soft-skills
---

Ever create a Test Strategy full of information, insight and hard-won experience only for no one to read it? I certainly have! It is frustrating for both the writer and the reader. How can we create Test Strategies that are more thought-provoking, engaging and encourage the reader to carry on reading? There are multiple factors to consider. The first we should start with is understanding our reader.

# Know Your Readers

When writing we typically think of our readers - sometimes without realising it. What is the reader's goal for an email, document, story or letter? Is it to understand something new, be entertained or informed? How can we tailor our writing to help them achieve that goal?

Yet testing strategies teams write with little consideration of the reader, often following the same strategies they have seen elsewhere. But much like any other type of writing, different readers will have different goals. By considering the goals of different readers we are more likely to write a test strategy that helps readers achieve them, becoming more relevant and valuable.

<Youtube Video - The four types of test strategy reader>

# The Four Types of Test Strategy Reader

When writing a test strategy, I anticipate up to four types of readers with differing goals. The four readers are:

  * Your Team
  * Related Teams
  * Internal Stakeholders
  * Regulators
  
The readers then can be compared in a matrix across expected detail and formality:

![Test Strategy Reader Types Matrix](/assets/img/2021/10/reader_type_matrix.png)

Let's consider each in turn.

## Your Team

<Youtube Video - What your team wants from a strategy>

Most test strategies should be read and understood by your team first. So your team is a natural first reader to consider. Your team will need to understand every element of your test strategy. When architecting a test strategy for your team be sure to include a good (but appropriate) level of detail. Consider not just How you test but also the Who, What, When, Where and Why. 

### Example Goals

  * Know the purpose of the project.
  * Appreciate testing priorities and risks.
  * Awareness of the team roles and responsibilities related to testing.
  * Understand all practical elements of testing on the team.
  * Understand team approach to test environments for testing internal and external to the team.

### Formality
But while your team might demand the detail, it is a challenge to keep engaging. Well, formality here is our friend. We don't need to be too formal with language getting creative with content design - avoiding that wall of text. Some ideas that can work in less formal contexts:

  * Include images and videos - not everyone learns best from text-based content.
    * Relevant Lightning Talks.
    * Diagrams from Blogs.
    * Be sure to reference the author!
  * Presentation Styles.
  * Chop up content into multiple easier to read sections.
  * Consider a Wiki style document instead of Word/PDF.

## Related Teams

<Youtube Video - What related teams want from a strategy>

Related teams are the ones who either have or provide a dependency on the work of your team. For example, a team that consumes your team's payments microservice. Related teams do not need or want every detail. Typically they are concerned with how to test the dependency with your team. We can help these readers by guiding them to the right content using techniques such as:
  * Highlight relevant strategy sections for related teams.
  * Create separate guidance documentation.
The goal is to help related teams filter out irrelevant test strategy information like how your team writes unit tests by combining filtering and editing techniques.

### Example Goals

  * Appreciate testing priorities and risks.
  * Awareness of the team roles and responsibilities related to testing.
  * Understand team approach to test environments for integration testing.

### Formality

Typically we don't need to be too formal with related teams. We can be creative in how we present information. Use the same techniques used with your team. But in a way more tailored to the related team's goals.

## Internal Stakeholders

<Youtube Video - What internal stakeholders want from a strategy>

Internal Stakeholders are anyone who has an interest in your teams work but no direct relationship to it. It could be the Head of Engineering or perhaps a tester in another unrelated team. They are interested but typically only at a high level. Internal Stakeholders want to know why your team exists, a summary of testing risks and who is involved. They do not need the additional detail of how or why.  But we should be careful with the tone used when speaking to them.

### Example Goals

  * Know the purpose of the project.
  * Appreciate testing priorities and risks.
  * Awareness of the team roles and responsibilities related to testing.

### Formality

Because Internal Stakeholders range from peers to leadership, we should carefully present information. Too informal can be misinterpreted as a casual attitude to testing and quality. But being too formal can put off our and related teams from reading. Depending on the formality of your team's testing strategy, consider a separate document for internal stakeholders. Summerise the testing strategy and where they can find more information if required. This way formality adapts, to different reader's needs. However, providing a transition point for those internal stakeholders who do want to understand more.

## Regulators

<Youtube Video - What regulators want from a strategy>

Regulators want to know it all. Regulators require detail to at least the same level as your team, and sometimes more.

Formality is also very different to the other types of readers. Specific requirements define how a test strategy and supporting documents, must be written. On top of this, a test strategy written for a regulator can also be a public document.

### Example Goals

  * Know the purpose of the project.
  * Appreciate testing priorities and risks.
  * Awareness of the team roles and responsibilities related to testing.
  * Understand all practical elements of testing on the team.
  * Understand team approach to test environments for testing internal and external to the team.
  * Legal/Regulatory compliance.

### Formality

Here we must typically adopt a very formal tone. Often defined by the regulator. The challenge, in this case, is how do we create a test strategy which our other types of readers will also find valuable? Here we should consider tactics to help bridge the gap between the specific goals of a regulator and other readers:

  * Highlight & colour code sections relevant to different types of readers.
  * Create separate summary documents for other teams based on the regulator document.
  * Presentations
  * Q&A sessions

# Understanding Your Readers Goals Makes Test Strategy More Relevant

Tailoring our test strategy to the goals of those we expect to read increases relevance. Meeting the needs of the reader helps them make better and more valuable decisions when testing. It also increases reader engagement as the reader gets what they need from the document. Not something generic or vague.