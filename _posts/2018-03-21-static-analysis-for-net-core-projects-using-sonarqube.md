---
title: Static Analysis for .NET Core Projects using SonarQube
date: 2018-03-21T13:54:00+00:00

layout: single
categories:
  - .NET Core
  - CI
  - qa
  - SonarQube
---
Static analysis is a way of automatically analysing code without executing it. As a development team, this is really powerful as once the static analysis software is up, running and integrated with your deployment pipelines you can gain an extra tester in your team with little ongoing maintenance! While some of the issues static analysis software finds are not always high value (code styling for example) some are issues your engineers are less likely to notice such as obscure security flaws and out of date dependencies.

## SonarQube; A Static Analysis Tool

[SonarQube](https://www.sonarqube.org/) is a static analysis tool that I have been using and evangelising at Just Eat. Some of the issues it finds:

  * Logic Bugs 
      * _Example_: Checking for null on an object that is always null.
  * Security Vulnerabilities 
      * _Example_: Passwords in the source code
  * Code Smells 
      * _Example_: Hardcoded URIs and Methods with a high [Cyclomatic Complexity](https://en.wikipedia.org/wiki/Cyclomatic_complexity) score.
  * Test Coverage 
      * SonarQube, however, does not calculate this by itself but instead [ingests test reports from your CI build](https://docs.sonarqube.org/display/SONAR/Seeing+Coverage).
  * Code Duplication

This information is all collated and displayed in a central dashboard for your project which gives you an overall view of the "quality" of your project. While some of the issues above might seem trivial (the code smells category is often guilty of this) even in these cases, monitoring the trivial metrics to see if they deteriorate over time is a useful measure for standards dropping within your team.

![Example SonarQube Project Dashboard](/assets/img/2018/03/SonarQube_Project_page.png)

### Quality Gates

Related to dropping standards are what SonarQube calls Quality Gates. Using these you can set triggers to throw either warnings or errors in your CI builds based on rules set in your Quality Gate. Example rules include:

  * Code Coverage below X%
  * Bug Count increased by X from the last build
  * Vulnerability Count increased by X from the last build

If any of these rules are broken you can choose to throw warnings or errors during your build process. Sonarqube can even be set up to break your build. But in my opinion, this isn't a good idea.

### The Case Against Breaking the Build

[BuildBreaker](https://github.com/SonarQubeCommunity/sonar-build-breaker) is an official SonarQube plugin which you can use to break your CI builds if a Quality Gate triggers any errors. On the face of it, this makes sense. You as a QA want your developers to maintain high standards so stopping them from breaking the Quality Gate rules by stopping there build from succeeding is an easy way to do this.

But if only it were that simple. Setting up SonarQube in this way has some key disadvantages:

  * It encourages the often observed us vs them dynamic between developer and QA.
  * In continuous delivery environments, you are now holding up a build. In the best case, the Quality Gate has detected a serious drop in quality or worse case trivial issue(s) have caused the build to fail. This won't make QA popular.
  * Breaking the build is likely to discourage developer buy-in. Without buy-in from your team, the issues found by SonarQube will never be resolved.

SonarQube should be used as a passive monitor of the health of your projects. By using it in this way you can start to work with your team rather than against them and use the metrics SonarQube discovers to start having conversations about how things might improve and even get involved in improving them yourself! SonarQube themselves did a blog post ["Why You Shouldn't Use Build Breaker"](https://blog.sonarsource.com/why-you-shouldnt-use-build-breaker/) with similar opinions.

### Github Integration

The final feature of SonarQube you should be aware of is it's GitHub integration. With the [Sonar-Github](https://github.com/SonarSource/sonar-github) plugin, you can set up integration with Github to comment on Pull Requests (PR) with issues found by SonarQube in the changes during your CI builds.

![SonarQube and GitHub integration example.](/assets/img/2018/03/sonarqube_PullRequestAnalysis.png)

One issue to note is you will probably want to differentiate between PR builds and builds of your _master_ branch.

SonarQube keeps a track of your latest build results to compare the next build to for purpose of its Quality Gate. However, for PR builds you probably don't want the results stored as you want to always compare the PR build to latest results from _master _otherwise a developer could just rebuild their branch in CI and the new issues previously found would no longer be new and disappear! Below is a PowerShell script I have used in teams to do this differentiation between PR and master branches:

```powershell
$github_branch_refs_parts = "%teamcity.build.branch%" -split "/"
$is_pr = ($github_branch_refs_parts.Count -eq 2 -and $github_branch_refs_parts[1] -eq "merge")

if (-Not $is_pr) {
    Write-Host "Running SonarQube in master branch mode"    
    SonarQube.Scanner.MSBuild.exe begin /k:"%sonar.project%" /d:"sonar.host.url=%sonar.host.url%" /d:sonar.cs.dotcover.reportsPaths="dotCover.html" /v:"%build.number%"
} else {
    Write-Host "Running SonarQube in PR Mode"

    $pull_request_number = $github_branch_refs_parts[0]
    $repo = "%repo_owner%" + "/" + "%name%"

    $command = 'SonarQube.Scanner.MSBuild.exe' +
    ' begin' + 
    ' /k:' + '%sonar_project%' + 
    ' /v:' + "%build_number%" +
    ' /d:sonar.host.url=' + "%sonar_hosturl%" +
    ' /d:sonar.github.pullRequest=' + $pull_request_number +
    ' /d:sonar.github.repository=' + $repo +
    ' /d:sonar.github.oauth=' + "%sonarqube_github_oauth_token%" +
    ' /d:sonar.analysis.mode=' + "preview" +
    ' /d:sonar.scanAllFiles=' + "true" +
    ' /d:sonar.github.endpoint=' + "%github_api_endpoint%"

    Write-Host $command 
    Invoke-Expression $command
}
```

The key difference between the two _SonarQube.Scanner.MSBuild.exe_ commands is in the analysis mode [_Preview_](https://blog.sonarsource.com/analysis-vs-preview-vs-incremental-preview-in-sonarqube/) the results are not saved by the SonarQube server so the comparison is always done against the latest _master_ build instead.

#### Analysis Mode Preview Deprecated in SonarQube 6.6

The Preview option is being deprecated according to the [documentation](https://docs.sonarqube.org/display/SONAR/Analysis+Parameters), however, I have not seen an alternative proposed yet so cannot suggest how you might handle this in SonarQube 6.6+.

## Setup SonarQube with a .NET Core Project

SonarQube now [supports .NET Core](https://www.sonarsource.com/resources/product-news/news.html#2017-04-13-sonarqube-scanner-for-msbuild-2-3-released) as of SonarQube Scanner for MSBuild version 2.3. So the setup is actually quite simple:

  1. Install the SonarQube Scanner on your CI server. I have used a build step for this and used [Chocolatey](https://chocolatey.org/) to manage the package installation.
  2. Before running your build step add another step which calls _SonarQube.Scanner.MSBuild.exe begin_ so SonarQube can setup hooks into your projects build process. Using the script above might be a good starting point.
  3. After the build process is completed end your SonarQube scan. This can be done with:  
    > _SonarQube.Scanner.MSBuild.exe end_

  4. During the end step the SonarQube scanner will upload a report to the SonarQube server and your projects dashboard will be updated.

And that is it! Well almost&#8230;

### Setting Up a Project Guid

For SonarQube to recognise your project from other projects it needs an identifier. The development team decided to use the ProjectGuid property in your .csproj file. You might not have one as they are not required by default. So double check your csproj files and update them to include a ProjectGuid property. If you miss this you will see the following error in your CI logs:

> <i class="mark error_msg ">WARNING: The following projects do not have a valid ProjectGuid and were not built using a valid solution (.sln) thus will be skipped from analysis&#8230;</i>

If you see that warning add your ProjectGuid!