---
title: Introduction to Automated Security Testing with OWASP Zap, Dependency Checker and Glue.
date: 2019-04-09T17:44:49+01:00
author: Thomas
layout: single
categories:
  - Uncategorised
tags:
  - owasp
  - security
---
Security testing can be really time-consuming. Ever tried to organise a penetration test for your website? It is expensive! For my current client, we wanted to think about how much security testing can be done ahead of time in an automated way. Not as a replacement for professional penetration testing but as a way to give us some confidence before that stage that we are catching issues as early as we can.

I did this by adding automated security tests for common issues in our codebase. For example, insecure dependencies or API endpoints that are vulnerable to SQL injection attempts. The Open Web Application Security Project (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://www.owasp.org/index.php/Main_Page" target="_blank">OWASP</a>) has a couple of tools that can help with this. **OWASP Dependency Checker, ZAP and Glue**. In this post, I will introduce them all and how they are meant to work together.

## Dependency Checker - Verifying Code you Consume

<a href="https://www.owasp.org/index.php/OWASP_Dependency_Check" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">Dependency checker</a> does what the name suggests - it checks your dependencies looking for ones with known vulnerabilities. Once it finds some it will let you know what they are a link to the National Vulnerability Database (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://nvd.nist.gov/" target="_blank">NVD</a>). It is fast, easy to set up and gives you some confidence that your code is built on a solid foundation.

Checking your dependencies is one of the first things you should do when looking to add automated verification of your application's security - it is a quick win! Check the paper <a href="https://cdn2.hubspot.net/hub/203759/file-1100864196-pdf/docs/Contrast_-_Insecure_Libraries_2014.pdf" target="_blank" rel="noreferrer noopener" aria-label=" (opens in a new tab)">Unfortunate Reality of Insecure Libraries</a> to understand more about the scale of the problem.

## ZAP - Verifying Code you Write

With your dependencies checked what about your own code. Zed Attack Proxy (<a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project" target="_blank">ZAP</a>) is the tool for this. It checks your code by doing both passive and active attacks against your site or API. Passive attacks are things like information disclosure such as your server version in the headers. In contrast, active attacks directly attack your application using attack vectors such as SQL injection.

One thing to keep in mind is the Active attacks can cause your site issues - after all, they are malicious requests! So it is best to run this tool against a test environment rather than the live site.

## Glue - Bringing Results Together

The two tools above will produce plenty of results to look at. But like all security testing tools, they produce false positives. Without a clear way to manage this, it can become painful quickly. <a rel="noreferrer noopener" aria-label=" (opens in a new tab)" href="https://www.owasp.org/index.php/OWASP_Glue_Tool_Project" target="_blank">Glue</a> helps with this by processing the output of Dependency Checker and Zap and publishing the results somewhere for you to review and if need be mark issues as false positives.

For example, in my setup, I set up glue to interact with the JIRA project for my team. Now once the security tests are completed the issues found are automatically raised in JIRA where engineers can review them. By doing this we make sure test results are addressed and any false positives can be marked as such.

Glue will even run a lot of tools for you. Although I had more success with [Dynamic Tasks](https://github.com/OWASP/glue/blob/master/docs/dynamic_task.md) and would recommend them instead of using the built-in ones. 

## Summary

Using the three tools together as part of your CI pipeline gives you the ability to address security issues sooner than you might usually. Although it is important to remember that all security tools report false positives and do not catch everything so in my opinion these tools are best used to complement a professional security review for your project. But if you haven't the budget for one of them then these tools might help you get some confidence!