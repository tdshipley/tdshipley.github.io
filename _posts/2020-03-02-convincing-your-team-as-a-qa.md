---
title: Introducting Change as a QA
date: 2020-03-02T15:21:31+01:00
author: Thomas
layout: post
categories:
  - change
  - soft skills
tags:
  - change
  - soft skills
---
## "How Do I Convince My Team to Do This?"
I was asked this question after presenting my [talk on Consumer-Driven Contract Tests](https://tomdriven.dev/events/) at London Tester Gathering. It is a great question. People generally don't like change and even less so when the concept is unfamiliar.

The question went on to ask (paraphrasing) - **"How do I approach the Delivery Leads about getting the time to do this?"**

*That is your first mistake!* Delivery Leads, Tech Leads, Product Owners, maybe even QA Managers have different goals to you the QA in the team. Yes we all hopefully want to deliver quality software but approach it in different ways.

## The Two Objectives of a Software Project
There are ultimately two objectives of a software project **deliver software** that is of sufficient **quality**. The contentious point being it is *quality*. What you as a QA consider as ready to release will be different from that of a Lead type role and that is ok.

The primary role of a **QA** in a team is to champion *quality*. The primary role of a **Lead** is to *deliver*. Of course, both roles care about each point but if you had to pick that is how it typically falls.

So when you ask your Lead **Can I have time to investigate this new Idea?** they naturally might push back - worried about delivery timescales.

## The Secret - Don't Ask
The best advice I have ever been given was the old adage:

> It is easier to ask forgiveness than seek permission. - [Grace Hopper...](https://quoteinvestigator.com/2018/06/19/forgive/)

Guess what - it is true! So below is my approach based on this advice to trying to convince people of a new idea.

### Disclaimer
This is my own personal approach and not all people and companies are the same. Don't just blindly follow what some stranger says on the internet. You will be taking time away from delivery following this approach so try not to do it around important deadlines. Use your own judgement.

That said you should definitely give this approach a go. You as a QA are the champion of quality so should try new ideas in defending it.

*If you find yourself in a place where you are so micromanaged that you cannot have any little side projects in work consider moving on. I have worked in places like that and generally found they are not worth sticking around.*

## Step 1 - Talk About Your Idea with your Colleagues
My most recent example of this approached is based on my work at John Lewis with Equal Experts. I wanted to introduce Consumer-Driven Contract Tests - but it was met with some skepticism.

So firstly, speak to others who might agree it is a good idea. Discuss the idea with them - ask lots of questions see if it is as good as you think. If even the people you thought would agree do not then think about why. Maybe this is not a good idea.

Try a different angle and refine until someone agrees. You can move onto step two without agreement but the risk of it not working out increases.

## Step 2 - Create a Very Small and Simple Proof of Concept
Now you have found some agreement work with them to come up with a simple working solution to at least part of your problem.

In John Lewis, it was another QA in another team. We worked together to create a very simple Consumer-Driven Contract Test and set up a simple [Broker](https://github.com/pact-foundation/pact_broker) to go with it.

Now you have more than just an idea. You have something you can show people as well. This is ideal for the next stage. It frames the discussion and will help people get over the psychological barrier of taking the first step.

## Step 3 - Showcase Your Work
Demo your simple proof of concept to your teams. If you have a related community (such as a weekly QA catch up) demo it there too. Speak to people about it. Get feedback.

As you get the feedback you may find that other people want to be involved. If you do great! This likely means you are solving a problem others have.

In John Lewis after some demo and promotional work, the idea gained momentum. Now there is a post on the [John Lewis Engineering Blog](https://medium.com/john-lewis-software-engineering/consumer-driven-contract-testing-a-scalable-testing-strategy-for-microservices-3f2b09f99ed1)

After doing all this showcase work you should hopefully have a proven out idea to take to your lead.

## Step 4 - Speak to Your Lead(s)
Now is the time to ask your Lead for time to investigate this idea further. Show them the proof of concept and how the idea has gathered momentum after you demoed it to your fellow QAs or Developers.

They will of course still be thinking about delivery. But it is a lot harder to dismiss an idea with momentum behind it.

## But it Might Not Work Out

At any of the stages above your idea may not work out. Some time was spent but it didn't help with delivery or quality. That happens in software all the time - not all ideas are winners. But you probably learnt about:

* Critical analysis
* Technologies
* Testing concepts
* Presenting to an individual or group
* Managing expectations

That seems worth taking the risk to me. But if all else fails ask for forgiveness!


