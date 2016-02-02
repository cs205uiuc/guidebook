---
layout: page
title:  "Setting up your gitlab"
---


# First Time Setup

If you are setting up your gitlab for the first time, you will need to create
a private "copy" of the CS 205 workbook.  To do this, you will create a **fork**
of the workbook.  To do so:

1. Go to the CS 205 workbook in gitlab:
    - [https://gitlab-beta.engr.illinois.edu/cs205-sp16/workbook](https://gitlab-beta.engr.illinois.edu/cs205-sp16/workbook)
2. Click **fork** to create your own copy of the workbook.
3. Once the repository is forked:
     - Click **Members** on the menu on the right hand side
     - Search for **waf** and add Wade as a **Reporter**
     - Search for **c-heeren** and add Cinda as a **Reporter**
     - *This allows us to have read-access to your files.*


# Cloning the Workbook

After you have forked your copy of the workbook, you need to download the workbook
to your CS 205 directory:

1. Open up your command line interface
2. Navigate to your cs205 directory
3. Run `git clone https://gitlab-beta.engr.illinois.edu/NETID/workbook.git`
    - Make sure to replace NETID with your NetID
4. Run the following command to add a new remote:
    - `git remote add release https://gitlab-beta.engr.illinois.edu/cs205-sp16/workbook`
