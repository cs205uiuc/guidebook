---
layout: page
title: "Reddit API in Python"
---

The Reddit API has an implementation in Python. This is called [PRAW](https://praw.readthedocs.org/en/stable/).
The documentation outlines how to work with the API.

# Getting Started working with the Reddit API in Python

To start, you will need a Reddit account so if you do not already have one, visit [this page](https://www.reddit.com/login)
and fill out the information under "Create a new account".

<img src="reddit-signup-page.png" style="border: solid 1px black;" />

Once you have this information, log in then click "Preferences."

<img src="reddit-prefs-link.png" style="border: solid 1px black;" />

At the top, click the apps tab.

<img src="reddit-apps-link.png" style="border: solid 1px black;" />

You should see a list of authorized applications (if you have authorized any).
Now scroll down to the bottom until you see "Developed applications" and click "Are you a developer? Create an app..."

<img src="reddit-app-reg.png" style="border: solid 1px black;" />

Fill out the information in the boxes. The redirect URL needs to be entered as shown and the app type
should be "script" but everything else can be whatever you want it to be. The about URL can be blank.
Once you are done, click "Create app"

<img src="reddit-app-reg.png" style="border: solid 1px black;" />

Once you have done this, you will need to obtain your client ID and client secret for the app.
To do this, find your app and if it isn't expanded already, click "edit". Then find your client
ID and client secret and put them in a safe place.

<img src="reddit-creds.png" style="border: solid 1px black;" />

# Setting up the libraries

To continue, you will need to install a couple of libraries that will let you work with the
API in Python
