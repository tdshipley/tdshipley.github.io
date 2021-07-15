---
title: Introducing Machine Learning for QA Engineers
date: 2018-01-24T09:00:47+00:00

layout: single
categories:
  - machine learning
  - qa
---
I believe it is a reasonable prediction that QA is one part of the software industry which will be disrupted by Machine Learning. And the role of a QA engineer will change as a result so it is important to have a grasp on the basics. This post will give you a high-level introduction to machine learning and the companies in the space working on changing how we assure quality.

# What is Machine Learning

[Arthur Samuel](https://en.wikipedia.org/wiki/Arthur_Samuel) a pioneer in Artifical Intelligence supposedly defined Machine Learning as:

> _Machine learning is a field of computer science that gives computers the ability to learn without being explicitly programmed._

But as always in computing, there are multiple techniques to give a computer the ability to learn.

# Types of Machine Learning Solution

There are three main types of machine learning solution.

## Supervised

In supervised learning, the developer has a set of known input and output data which is known as training data. Then the solution follows this typical pattern:

  1. Process the training data through the code to create a model of the data and get the predicted outputs.
  2. Compare the predicted output with the known output to get a value representing the accuracy of the machine learning model.
  3. Based on the accuracy adjust the model and run it against the training data again to get an updated value for model accuracy.
  4. Keep repeating steps 2 & 4 until target accuracy has been reached.

Supervised learning problems can be further categorised into two categories _Categorisation _and _Regression_.

### Categorisation

Categorisation problems focus on answers to questions. Given some input data is the output yes or no?

#### Examples

  * Advertising - given what we know about the user, will they then click on the advert?
  * Spam Filters - given what we know about this email, is it a spam email?

### Regression

Regression, on the other hand, aims to give a prediction between two floating numbers such as 0.00 & 1.00. Here we model is trying to predict a value.

#### Examples

  * House Prices - given what we know about a house, what is its predicted value?
  * Stock Prices - given what we know about a company, what is the predicted value of its stock?

## Unsupervised

Unsupervised learning differs from Supervised as there is no training data of known inputs and outputs to train a model (learn) from. Instead, the code looks for patterns and relationships in the data that it can learn from.

Unsupervised learning problems can also be broken down into two categories _Clustering_ and _Association_.

### Clustering

In clustering, the model is looking for groups in the input data.

#### Examples

  * Customer Behaviour - given what we know about a customer and their behaviour what group of other customers are they similar to.

### Association

With association problems, the model is looking to find rules that describe the data.

#### Example

  * Customer Behaviour - given what we know about customers of our company what general rules can be applied. Such as if a customer buys A they will also want to buy B.

## Reinforcement

Reinforcement learning is a blend of supervised and unsupervised learning. It is similar supervised learning because once the code has been executed the model is updated based on the output this, is where the reinforcement comes from. However, unlike supervised learning the developer has no known input data - this is the similarity with unsupervised learning.

### Example

  * Buying stocks - given what we know about a company, its share price and our last hold, buy and sell decision will we make a profit if we hold, buy or sell this time?

# Companies Working on this Problem

There are many startups and companies working on this problem right now:

  * [Appdiff](https://www.appdiff.com/) raised [$2,500,000 in seed capital](https://www.crunchbase.com/organization/appdiff/funding_rounds/funding_rounds_list) to try and reduce the time spent by companies on manual and automated testing.
  * [SOFY.AI](http://SOFY.AI) is working on a machine learning solution to learn how to use mobile apps in iOS and Android to reduce manual and automated testing.
  * [AppAchhi](https://appachhi.com/) also offers a product that learns how to use your mobile app and find non-functional issues automatically to augment your automated tests.
  * [Unravel](https://www.unravel.io/) allows testers to write automated tests in English like syntax and uses machine learning techniques to reduce maintenance of tests by learning about your website to understand changes and update your tests.

# How QA is Being Impacted by Machine Learning Now

Looking at the companies above it looks like right now a lot of effort is being spent on mobile application testing. This I think makes sense for two reasons:

  1. Lots of companies are focusing on their mobile applications right now and so it makes sense that software companies are looking for new ways to improve the quality of these apps and earn some of the development budgets!
  2.  In my experience mobile QA is a little behind technology available in other architectures such as web applications. These companies are looking to innovate in the mobile QA space to capitalise on this.

However, it is not just mobile QA which is receiving attention but also areas such as web development by companies like [Unravel](https://www.unravel.io/) who are looking to augment their technology with existing automated testing frameworks to make them more robust.

# How QA Could be Impacted in the Future

Clearly, no one can predict the future but we can look at the above and extrapolate out. Personally, I believe we will see:

  * More augmentation services looking to improve your automated tests to make them less flakey and more resilient.
  * Continued work to replace manual testing of mobile applications and in the future other types of UI driven application such as web applications. Manual testing is hugely expensive and any company which can automate it away is likely to make a lot of money.
  * Non-functional testing is all about looking for patterns and this is something [AppAchhi](https://appachhi.com/) is looking at right now and I think given how suited it is to unsupervised learning this will only continue.

In short, the role of a QA is not going to go away but I believe the number of manual test positions will reduce to just what is needed for human based exploratory testing while the role of a QA Developer will shift from maintaining test suites and tooling to architecting the right machine learning solutions and making customisations where necessary.

# Learn More

  * <a href="https://www.aitesting.org/" target="_blank" rel="noopener"><span style="font-weight: 400;">Artificial Intelligence for Software Testing Association</span></a>
  * <a href="https://www.coursera.org/learn/neural-networks-deep-learning" target="_blank" rel="noopener"><span style="font-weight: 400;">Coursera - Neural Networks and Deep Learning</span></a>
  * <a href="https://hackernoon.com/learning-ai-if-you-suck-at-math-8bdfb4b79037" target="_blank" rel="noopener"><span style="font-weight: 400;">Learning AI if you Suck at Math</span></a>
  * <a href="https://docs.google.com/presentation/d/1kSuQyW5DTnkVaZEjGYCkfOxvzCqGEFzWBy4e9Uedd9k/preview?imm_mid=0f9b7e&cmp=em-data-na-na-newsltr_20171213&slide=id.g168a3288f7_0_58" target="_blank" rel="noopener">Jason Mayes - Machine Learning 101</a>