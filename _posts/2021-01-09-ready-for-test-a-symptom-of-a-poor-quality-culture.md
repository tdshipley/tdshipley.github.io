---
title: Ready for Test - a Symptom of a Poor Quality Culture 
date: 2021-01-09T12:31:32+01:00
author: Thomas
layout: post
categories:
  - leadership
tags:
  - leadership
  - team-culture
  - soft-skills
---
The Ready for Test column on your JIRA/Agile/Kanban/Whatever process feels safe, doesn't it?
It is a well-known column and on the surface seems to follow nicely with how tickets are worked on.
There is a bit of elaboration, then some code is written (hopefully reviewed) and finally
we can move it into QA where an independent set of eyes can take a look at it. But doesn't it
all sound a little less Agile and a bit more Waterfall?

Ideas such as Shift Left, Continuous Integration and DevOps are increasingly popular. Their popularity
stems from early feedback, sharing knowledge and ownership between team members. Yet Agile software
teams continue to treat QA concerns as a separate stage owned by different people. All the benefits of
the Agile ways of working above give us are lost. QA team members provide feedback after the task,
hoarding knowledge and being passed ownership of quality.

In this post, I want to convince you that in a lot of cases Ready for Test, In QA and other quality
gates do more harm than good. They contribute to a culture of separation between QAs and other team
members. This separation causes quality to decrease.

## Quality is the Concern of All

Let us start with the basics. Everyone on the team has a responsibility to deliver a quality product.
That is not something specific to our industry but is true in near all industries. A well-performing team
works together and helps each other to achieve a goal whether that is a successful Sprint in IT or
on the Athletic track.

So here is the first issue with Ready for Test. If we all have a responsibility to deliver good work then why
hasn't the work been ready for testing from the first step? And why should a specific person check that work?

Testing is more than checking the nuts and bolts fit together. It is also discovering if those nuts and bolts
should be put together and if it is being done in the right way.

## Testing Early and Continuously

This brings us onto early testing. How can we question design and method early on before we as a team
test functionality? As development continues the approach will change, how can we verify this change?

### Three Amigos

Get some people in a room - canonically a developer, QA and BA/Product Owner. At the start of a piece of work
discuss the aims and the constraints. Talk about the concerns of the ticket be it testing, business or user ones.
Note down on the ticket any important points.

You are testing assumptions and the shared understanding of the work. Clearing up misunderstanding early on
saves time later on fixing defects and bugs.

### Pairing

Once upon a time, I was sat in a retro with my team. I wanted developers on the team to be more available for pairing
and working on testing tasks. Some of the developers weren't too happy. They wanted to focus on feature work. Not
"QA" work.

> "If we are meant to pair on Test tickets then that means you should be pairing on Dev tickets?"

**Yes!** Pairing is a great way to test things early and importantly should work both ways.

QAs should pair with developers on feature work asking questions about implementation and improving there understanding.
Equally, Developers should be doing the same. We don't want silos in software development. We want knowledge to be spread
across the team so if one person leaves its not a mad dash to take on knowledge transfer tasks.

### Discovery / Spike Tickets

Sometimes the team doesn't know enough about a problem to deliver on the shared promise of quality. In these cases, someone
will suggest a Spike or Discovery ticket. A timeboxed assigned task to someone to investigate and return with more
information for the team so an informed decision can be made.

These types of tasks are all about testing. Testing an idea, evaluating options and returning a conclusion. They are also
a natural fit for Pairing. Devs and QAs should work on these spikes to make sure the correct questions are being asked,
the right options are evaluated and results are presented from a multifaceted view.

## Manual and Automated Testing - a Separate Stage?

If everyone owns the quality of delivery then everyone owns the verification of that quality right? You cannot have shared
ownership of something if only a handful of people verify it. The teams should as a whole be questioning if a suitable
level of quality has been achieved before release.

This brings me to testing. A developer doesn't need a QA to test anything. There is evidence of this already - when the
developers on a team write unit tests. This task is managed easily. There is no reason why a developer working on a task
cannot also write some functional automated tests. Perhaps they could also do a manual check if required.

I can hear the pushback through my screen. *"I shouldn't test my own work - separation helps find defects."* I agree. But that
separation doesn't need to be from a QA - it certainly doesn't need to be a separate stage. It should already be happening.
**Quality is a feature, not an afterthought.** Anyone can pair on testing activities and they should be doing so early and throughout
the progress of a ticket. Pairing, Three Amigos, Spikes will all allow you to do this.

## There is no Ready for Test - It Already is

We have seen techniques to allow us to test early and continuously. If we have been utilising them then what is left? Not much.
Testing has been constant, a pair of team members have been working together on a ticket which was well understood because we
either held a Three Amigos session to avoid misunderstandings or a Spike.

Ok, there might need to be some final checks driven by how much risk is associated with the work. That is what Demo sessions are for.
Demo to your squad, your team, your product owner. A bit nervous before the demo? Grab a team member and demo it to just them -
if it makes you feel better to call it pairing!

## FAQ

### So What is the Role of a QA?

Ok, I have now talked myself out of a job it seems. Sometimes - but more often not.

QAs on a team are typically outnumbered by other team members. They cannot be involved in everything
and shouldn't be. Their time is better spent shepherding the team towards shared ownership of quality and
ensuring that collective responsibility is established. Someways this can be done:

* Pairing with Developers
* Doing Discovery work to Enable Better Testing
* Setting up Test Infrastructure to make it easier for others to Test
* Liaising with Testers in other teams
* Reviewing user feedback. Bringing that information to the team
* Running Three Amigos/Retro/Standup sessions
* Testing high-risk features where extra reassurance is needed

### Where should I put Testing Tasks on the Board?

Treat these tickets like any other ticket. Ready for development, In Progress. Testing tasks don't need a special
column all of there own. It only serves to encourage testing to be the responsibility of a small subset of
the team.