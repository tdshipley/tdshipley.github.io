---
title: Creating a Visual Studio Code Task for Building a .NET Core Project
date: 2016-03-20T13:18:32+00:00

layout: single
categories:
  - .NET Core
  - 'C#'
  - Visual Studio Code
---
[Visual Studio Code](https://code.visualstudio.com) is a great new multi-platform code editor from Microsoft currently in beta. It is a lot more lightweight than Visual Studio.

But when writing code I in VS Code I missed the Ctrl-Shift-B shortcut. It makes sense that VS Code doesn't have it - after all, it doesn't know what is being written and the build targets, and you can always build without it in .NET Core using _dnu build_ but it can be added back in.

## Visual Studio Code Tasks

Turns out you can integrate your own tasks into VS Code - when combined with [Gulp](http://gulpjs.com) it becomes easy to map Ctrl-Shift-B (or Cmd-Shift-B on a Mac) to _dnu build_. Scott Hanselman has a good guide called:

<p class="blogTitle">
  <a class="TitleLinkStyle" href="http://www.hanselman.com/blog/IntegratingVisualStudioCodeWithDnxwatchToDevelopASPNET5Applications.aspx" rel="bookmark">Integrating Visual Studio Code with dnx-watch to develop ASP.NET 5 applications</a>
</p>

Which can guide you through the process. But it only works if your gulp file is also at the root of your project. What if it is located elsewhere - like in the src directory?

## Specifying the Current Working Directory

If you take a look at the [Tasks.json schema](https://code.visualstudio.com/docs/editor/tasks_appendix) there is _Command Options_ interface which has two properties - one of which is _cwd_ - current working directory. This can be combined with [Variable Substitution](https://code.visualstudio.com/docs/editor/tasks#_variable-substitution), which gives access to values like the workspace root.

So in a task add an options object with a cwd property which points to the folder containing your gulp file - an example is below:

```json
{
    "version": "0.1.0",
    "command": "gulp",
    "isShellCommand": true,
    "options": {
        "cwd": "${workspaceRoot}/src/MyProject"
    },
    "tasks": [
        {
            "taskName": "dnu-build",
            "isBuildCommand": true,
            "showOutput": "always",
            "isWatching": true
        }
    ]
}
```

Now, this gulp task will be assigned to Shift-Ctrl-B and run within the working directory of ./src/MyProject using the gulp file within that folder.