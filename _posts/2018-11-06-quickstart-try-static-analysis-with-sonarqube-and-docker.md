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

```bash
docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube
```

The output of this command should look similar to:

```bash
Unable to find image 'sonarqube:latest' locally
latest: Pulling from library/sonarqube
bc9ab73e5b14: Pull complete 
193a6306c92a: Pull complete 
e5c3f8c317dc: Pull complete 
a587a86c9dcb: Pull complete 
a4c7ee7ef122: Pull complete 
a7c0dad691e9: Pull complete 
367a6a68b113: Pull complete 
60c0e52d1ec2: Pull complete 
c9d22bc43935: Pull complete 
884af0bfbb9a: Pull complete 
35a8cd0c916a: Pull complete 
9f9ecbe7a343: Pull complete 
af800bded4f3: Pull complete 
Digest: sha256:cc57b262ee9e7145456dee8c7ae24622c82b22cabeaac4651e7dd642da806f2e
Status: Downloaded newer image for sonarqube:latest
a263b203864adc366919ba9cde3cde87542c96046af7a8b9d7ebc1f155ec2204
```

This will download the latest SonarQube image from Docker Hub and will set up a container using it. To start your server you just need to run this container.

# Run the SonarQube Docker Container

Now if you run: `docker container ls` in your command window you should see your container named _sonarqube -_ for example:

```
My-MacBook-Pro:kotlin thomas$ docker container ls
CONTAINER ID   IMAGE       COMMAND         CREATED           STATUS            PORTS                                            NAMES
68be74d0aa51   sonarqube   "./bin/run.sh"  About an hour ago Up About an hour  0.0.0.0:9000->9000/tcp, 0.0.0.0:9092->9092/tcp   gracious_noyce
```

Now you are ready to start the SonarQube server using the `docker run sonarqube` command. If this was successful you should see your command window fill with text about the server starting and once loaded be able to see the dashboard at `http://localhost:9000`. Now you can scan your project.

# Scan your Project with Sonar-Scanner

To have some results in your proof of concept SonarQube server you need to scan a project. [Sonarqube supports a host of languages](https://www.sonarqube.org/features/multi-languages/) so pick a project written in a supported language (you may need to install a plugin). Next, make sure you have the [Sonar-Scanner](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner) application which you can run from your command window. But before you run it at the root of your project add a _sonar-project.properties_ file. This will tell the scanner a bit about your project and where to send the results. Below is an example of the minimum required information:

```
#----- SonarQube server
sonar.host.url=http://localhost:9000

#----- Project Key
sonar.projectKey=4a27fa8c666747f6956d75ae63fb24b9

#----- Project Name
sonar.projectName=MyProjectName

#----- Project Version
sonar.projectVersion=1.0

#----- Source files (relative)
sonar.sources=.
```

The projectKey needs to be unique to your project on the SonarQube server and the rest is self-explanatory. With all this in place with your command line in the root of the project where the sonar-scanner is located (unless you have installed it in another way such as with [Homebrew](https://brew.sh/)) enter `sonar-scanner` and press enter. You will see an output like this:

```
My-MacBook-Pro:kotlin thomas$ sonar-scanner
<Redacted for brevity>
INFO: ANALYSIS SUCCESSFUL, you can browse http://localhost:9000/dashboard/index/4a27fa8c666747f6956d75ae63fb24b9
INFO: Note that you will be able to access the updated dashboard once the server has processed the submitted analysis report
INFO: More about the report processing at http://localhost:9000/api/ce/task?id=AWbpY5h5xoaTc7Huvu3D
INFO: Task total time: 4.403 s
INFO: ------------------------------------------------------------------------
INFO: EXECUTION SUCCESS
INFO: ------------------------------------------------------------------------
INFO: Total time: 5.628s
INFO: Final Memory: 11M/50M
INFO: ------------------------------------------------------------------------
```

Once completed your results will be in the SonarQube dashboard by following the link. Now start to play around with SonarQube and your team's projects!

