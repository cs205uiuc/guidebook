---
layout: page
title:  "Python Prerequisites"
---


CS 205 is “Data Driven Discovery”, where we will use data as the driver to discover new things.
In order to do this discovery, we are going to need some tools to help us out.
The most basic tool we will use is the Python programming language.
Python is a language that is particularly strong at processing data and has a massive
number libraries developed by other people that will help us processing that data.


# Installing Python (Miniconda)

Python itself is a programming language and you can install *just* Python.
However, we want to use both Python and libraries that others have developed.
For that, CS 205 uses a Python distribution -- a package that contains the
Python programming language along side tools to make the process of getting
libraries easier.  Specifically, we will use the Miniconda distribution.

1. Windows
  - [Download Miniconda here](http://conda.pydata.org/miniconda.html)
  - Run the installer, all the deafult options are fine

2. Mac OS X
    - [Download Miniconda here](http://conda.pydata.org/miniconda.html)
    - Once downloaded, you will need to launch your Terminal
      (see [Command Line](command-line.html))
    - Inside of the Terminal, run the following:
        * `cd Downlaods`
        * `bash Miniconda3-latest-MacOSX-x86_64.sh`
        * As you review the license, you can press `q` to exit the license screen
        * All the default options are fine


# Installing Jupyter

The very first tool we will use is Jupyter,  a tool that makes writing small
programs easier.  To get Jupyter, we will use a the ``conda`` package manager
that was installed as part of Miniconda:

1. Open up command line interface and navigate to your CS 205 directory
2. Run: ``conda install jupyter`` to install Jupyter
   (You will need to press ``y`` to confirm the install)
