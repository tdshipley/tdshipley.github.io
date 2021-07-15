---
title: How to Setup Anaconda on Mac OSX
date: 2016-09-19T17:04:31+01:00
author: Thomas
layout: single
categories:
  - Python
---
## What is Anaconda?

Anaconda is both a data science platform and distribution of Python. But its also a nice way of managing multiple versions of Python and Virtual Environments (in the same way as [VirtualEnv](https://virtualenv.pypa.io/en/stable/)).

## Installing

To install go to the [Anaconda Downloads](https://www.continuum.io/downloads) page and download the version dependent on the version of Python you would like. I used the graphical installer which is really straightforward.

### Only Use Anaconda Python in an Anaconda Virtual Environment

Once the install is complete if you reload your terminal and check your python version (assuming you installed Python 3):

```bash
python3 -V
>> Python 3.4.5 :: Anaconda 4.1.1 (x86_64)
```

This is fine if you want to use the Anaconda variant of Python all the time. But what if you want to use vanilla Python when not in a Virtual Environment? Perhaps you have a tool (like I did) which does not play nice with Anaconda.

To fix this open up your bash_profile:

```bash
open ~/.bash_profile
```

The file has been updated with a new statement adding Anaconda to the beginning of the path:

```bash
# added by Anaconda3 4.1.1 installer
export PATH="/Users/thomasshipley/anaconda/bin:$PATH"
```

Update this so that Anaconda is added to the end of your path:

```bash
# added by Anaconda3 4.1.1 installer
export PATH="$PATH:/Users/thomasshipley/anaconda/bin"
```

Restart your terminal and now the Anaconda variant of Python is only used when you are within an Anaconda Virtual Environment. To confirm this check your version of python the terminal:

```bash
python3 -V
>> Python 3.5.2
```

## Creating and Activating a Virtual Environment

Now you have Anaconda installed it is easy to create a virtual environment to work in:

``bash
conda create -n my_env python=3.4 anaconda
```

The command above is quite straightforward just pass an _-n_ flag for the name of your environment and specify the python version in the _python_ flag - in this case 3.4.

### Activate and Deactivate Your Environment

To activate your new environment:

```bash
source activate my_env
```

And to deactivate your environment:

```bash
source deactivate
```

Now you can switch between an unlimited number of environments with specific python versions easily.