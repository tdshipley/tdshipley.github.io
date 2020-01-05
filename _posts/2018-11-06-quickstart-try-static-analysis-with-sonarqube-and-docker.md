---
title: 'Quickstart: Try Static Analysis with SonarQube and Docker'
date: 2018-11-06T14:51:34+00:00
author: Thomas
layout: post
categories:
  - SonarQube
  - Uncategorised
---
Recently I started a new contract and was in the rare position of joining a team before the developers! Without a team producing work, I wanted to think about ways to get the team off to a good start. My last post was about static analysis with Sonarqube. I love static analysis tools they are like an additional tester in your team and when the results are taken in the context of the wider effort they can be really valuable. Below I want to show you how to set up a quick proof of concept Sonarqube server to discuss with your team.

# Overview

Before starting this guide I assume you have a superficial level of Docker knowledge (I am not an expert) and you have it installed. **There are three steps to getting started in total it will probably take 15 minutes** (excluding download times):

  1. Create a docker image with SonarQube installed using [Docker Hub](https://hub.docker.com/_/sonarqube/)
  2. Run the docker image just created.
  3. Install Sonar-Scanner and create a SonarQube properties file in the root of your project to run a scan.

# Create a SonarQube Docker Container

To use SonarQube you need to be running the server somewhere. We will use [Docker](https://www.docker.com/). It will download a docker image which contains SonarQube for us already configured and set it up as a container on your machine. To do this open your command window and type:

https://gist.github.com/tdshipley/a43d9ca82a309f6c793a200029fb7581

The output of this command should look similar to:

https://gist.github.com/tdshipley/5d2f410b8b07f8e2ae96f49a40d1f11b

This will download the latest SonarQube image from Docker Hub and will set up a container using it. To start your server you just need to run this container.

# Run the SonarQube Docker Container

Now if you run: `docker container ls` in your command window you should see your container named _sonarqube -_ for example:

https://gist.github.com/tdshipley/1680940db223e2d320acb2a2fec6098e

Now you are ready to start the SonarQube server using the `docker run sonarqube` command. If this was successful you should see your command window fill with text about the server starting and once loaded be able to see the dashboard at `http://localhost:9000`. Now you can scan your project.

# Scan your Project with Sonar-Scanner

To have some results in your proof of concept SonarQube server you need to scan a project. [Sonarqube supports a host of languages](https://www.sonarqube.org/features/multi-languages/) so pick a project written in a supported language (you may need to install a plugin). Next, make sure you have the [Sonar-Scanner](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner) application which you can run from your command window. But before you run it at the root of your project add a _sonar-project.properties_ file. This will tell the scanner a bit about your project and where to send the results. Below is an example of the minimum required information:

https://gist.github.com/tdshipley/e12f7287e83ce46aeafd2f80e9038656

The projectKey needs to be unique to your project on the SonarQube server and the rest is self-explanatory. With all this in place with your command line in the root of the project where the sonar-scanner is located (unless you have installed it in another way such as with [Homebrew](https://brew.sh/)) enter `sonar-scanner` and press enter. You will see an output like this:

https://gist.github.com/tdshipley/3c176fd45c8a9e7a092d7e3b332eaf63

Once completed your results will be in the SonarQube dashboard by following the link. Now start to play around with SonarQube and your team's projects!

