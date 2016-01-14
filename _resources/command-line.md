---
layout: page
title:  "Command Line"
---



If you think about how you usually use a computer, you probably navigate to a file by clicking
on directories and open a program or file by double clicking on them.  When you are programming
a computer, you often need to run programs and send them options, called arguments, which is nearly
impossible to do with only a click.

Because of this, every operating system contains a Command Line Interface (CLI) that lets you interact
with your computer using a keyboard.   You can do everything you already do on a computer via the
command line, but you can also do a whole lot more!


## Entering the command line

Every operating system comes with a command line tool, though the tool varies depending on your
operating system:


#### Windows

1. Press [Start] on your keybaord, or press the Start menu
2. Type the following: ``cmd``
3. Press [Enter]
4. "Command Prompt" will open, which is the default command line tool for Windows


#### Mac OS X

1. Press [Apple] + Space to bring up Spotlight, or open up Spotlight or App Launcher
2. Type the following: ``Terminal``
3. Press [Enter]
4. "Terminal" will open, which is the default command line tool for OS X



## Command prompt

Both command line tools start every line with a prompt that shows the current
working directory of the command line tool.  By default, both Windows and Mac
starts you off in the base folder for your user account.  The syntax varies
only slightly between the two (assuming a user named **Zephyr**), so the
initial prompt should be one of the following:

* Windows: ``C:\Users\Zephyr\>``
* Mac OS X: ``Zephyrs-MacBook-Pro:~ Zephyr$``


## Current working directory

When using the command line, you are always "inside" of one specific folder
(much like when you double-click a folder you see the contents of everything
in that folder and only that folder).  The current folder that your command
line tool is in is referred to as the *current working directory*.

In CS 205, we recommend that you work within a folder called ``cs205`` on
your desktop.  In order to navigate to that folder, we need to first navigate
to your Desktop and then navigate to the CS 205 folder.  Both of these
things can be done with the ``cd`` command (``cd`` for "change directory").

Inside of your command line tool:

1. Type ``cd Desktop`` to move from your home directory to your Desktop.
2. Type ``cd cs205`` to move from your Desktop into your cs205 folder.

You can visually verify that you are now in your CS 205 directory by looking
at the prompt:

* Windows: ``C:\Users\Zephyr\Desktop\cs205\>``
* Mac OS X: ``Zephyrs-MacBook-Pro:cs205 Zephyr$``


## Highly Useful Commands

### Listing files in your current directory

When using a command line tool, you often want to know what files are in
your current working directory.  To list all files in the current directory:

* Windows: ``dir``
* Mac OS X: ``ls``

### Changing directories

In addition to moving "forward" or "deeper" into your directories, there
are two special arguments to the cd command to help you navigate around
your computer.

1. To go “backwards” one directory, the special ``..`` (two periods) argument
   will move you back one directory: ``cd ..``

2. To go back to your starting directory, no matter where you are at on your \
   computer, you can always return home with the following special command:
  * Windows: ``cd %homepath%``
  * Mac OS X: ``cd ~``
