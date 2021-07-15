---
title: Finding Lost Commit History using the GitHub API
date: 2015-06-17T17:23:28+01:00
author: Thomas
layout: single
categories:
  - Git
  - GitHub
tags:
  - git
  - github
  - recovery
  - reflog
---
It is quite easy to lose commit history in Git. A mistaken forced push is enough to rewrite the past and lose valuable work. Assuming the user in question has not done a _[git fetch](http://git-scm.com/docs/git-fetch)_ in a while _[reflog](http://git-scm.com/docs/git-reflog)_ won't help you either.

This happened to me while dealing with a branch that had a misconfigured remote pointing to the mainline. In my stupor, I forced the push.

# Outdated reflog! Perhaps GitHub has the Answer?

All is not lost however you can access all the information you need via the GitHub API. Assuming you have stopped the team making anymore commits to the branch! You can attack the problem in the following order:

  1. Query the event log for the repository to find the hash of the last good commit.
  2. Request the branch with a detached HEAD at the point of the last good commit.
  3. Check this out as its own branch.
  4. Merge this branch containing this good history back into the original branch.

## Querying for Repository Events

GitHub has a get request you can run for [repository events](https://developer.github.com/v3/activity/events/#list-repository-events):

    GET /repos/:owner/:repo/events 

Using the _curl_ command in Mac OS X you can grab a JSON blob of events on that repo to find the hash of your last good commit:

    curl -u <github username> https://api.github.com/repos/<github repo owner>/<repo name>/events

Just replace the info in the angle brackets with your own.

You will be asked for a password this should be your GitHub password or if you have two-factor authentication switched on an application specific password with the appropriate permissions.

## Requesting a Detached Head Branch at The Last Good Commit

Now you hopefully have the hash of the last good commit this can be used to get a branch with a detached head at that commit. You can do this using a GET in the [GitHub References API](https://developer.github.com/v3/git/refs/):

    GET /repos/:owner/:repo/git/refs/:ref

Again using curl and this API call you can get the branch:

    ```bash
    curl -u <github username> -i -H "Accept: application/json" -H "Content-Type: application/json" -X POST -d '{"ref":"refs/heads/<NEW recovery branch name>", "sha":"<hash of the last good commit from previous request>"}' https://api.github.com/repos/<repo owner>/<repo name>/git/refs
    ```

As before just replace the angle brackets with your data. Note you need to pass a NEW branch name you intend to store this recovery on. You will also need your password or application specific one again.

## Checking out the Recovered Commits on Another Branch

Now if you do a _git status _you will see that the branch is in a detached state so check this into its own branch by running:

```bash
git checkout -b "the new branch name from the previous step"
```

At this point, the commits have been recovered and are on your local branch. The crisis is nearly over!

## Merge the Recovered Commits Branch into the Original

Now check out the original branch with the missing commit history and run a merge command:

```bash
git merge "name of the branch with the recovered commits"
```

If all goes well you can do a _git push_ to remote of the branch. If you are a little paranoid however that you are about to push to the wrong place again like I was you can always check your remote settings by running:

```bash
git remote show origin
```

Assuming your Git setup has the remote defined as the default _origin_ Else check your .gitconfig for the correct remote name to use.

Now the work should be recovered!