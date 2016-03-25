---
layout: page
title: "Cleaning text from Reddit in Python"
---

Let's say you've gotten some number of posts from various subreddits on Reddit. You now want to extract
something specific from that data (for example, links). In this guide, you will learn how to extract data
from a post.

# Getting the posts

Before we go into how to clean the text and get what you want out of it, let's back up and
show you how to get posts. To do this, you should come up with a list of subreddits to get
posts from and decide how many posts you want to get from each subreddit. To come up with
a list of subreddits, you could use the [list of default subreddits](https://www.reddit.com/r/defaults/comments/3hu24f/list_of_default_subreddits_20150821_multiple/)
or a [list of subreddits by subscriber count](http://redditlist.com/). It is not recommended to
select a large number of posts and subreddits as it would take a long time to actually get
the data from the API since the API is limited to 60 requests per minute. Once you have made
a list of the subreddits you wish to use, save it as a json file such as the example below,
replacing the example text with a comma separated list of subreddits.

```
[
"news",
"pics",
"food"
]
```

Now you can use that list to get posts. To do this, we need a new python program.
This can be done outside your workbook directory or inside of it. Do the following
to get the data to use for your project, changing the filename for
your subreddit list and the number of posts to be gotten to what you want to. We
will save each submission to a file.

```python
import praw
import OAuth2Util
import json
import os

# These functions are from https://github.com/NSchrading/redditDataExtractor/blob/master/RedditDataExtractor/redditDataExtractor.py
# They will help with cleaning out some problematic data returned from the API as well as making a list of comments
def get_submission_info(sm):
    sdata = vars(sm)
    if sm.author is None:
        sdata["author"] = "[Deleted]"
    else:
        sdata["author"] = sm.author.name
    sdata["subreddit"] = sm.subreddit.display_name
    sdata["comments"] = get_submission_comments(sm.comments)
    #The following are all objects, lists of objects or dictionaries of objects that we don't need anymore
    del sdata["_comments"]
    del sdata["_comments_by_id"]
    del sdata["reddit_session"]
    return sdata

def get_submission_comments(sComments):
    comments = {}
    for comment in sComments:
        if isinstance(comment, praw.objects.Comment):
            author = comment.author
            if author is None:
                author = "[Deleted]"
            else:
                author = author.name
            if comments.get(author) is not None:
                comments[author].append({"Body": comment.body, "Replies": get_comments(comment.replies)})
            else:
                comments[author] = [{"Body": comment.body, "Replies": get_comments(comment.replies)}]
    return comments

def do_compute():
  r = praw.Reddit("PostGetter") # The one argument being passed here is the user agent string which is required by the api
  o = OAuth2Util.OAuth2Util(r, configfile="YOUR_WORKBOOK_DIRECTORY/static/keys/oauth.ini") #if you are working within the workbook directory, change configfile to ../static/keys/oauth.ini

  #Change "your_list.json" in the following line to the name of the file where your subreddit list is stored.
  with open("your_list.json", "r") as list_read:
    subreddit_list = json.load(list_read)

  for sub in subreddit_list:
    try:
      os.mkdir(sub)
    except OSError:
      pass #Directory already exists so we catch the exception raised by os.mkdir() and move on
    cur_sub = r.get_subreddit(sub)
    for submission in cur_sub.get_hot(limit=7): #Change the value of limit to the number of posts you want to get
      filename = submission["id"] + ".json" #use the submission id as a filename
      with open(os.path.join(os.getcwd(), sub, filename), "w") as post_write:
        post_json = vars(submission)
        post_cleaned = get_submission_info(post_json)
        post = json.dumps(post_cleaned, indent=4)
        post_write.write(post)
```

Please note that it may take a long time to get the posts if you are attempting to get a large number of posts.

# Cleaning the data

Now that we have a set of posts to work with, we should clean up that data. To get started,
set up a new directory inside your workbook directory. Move the directories with the posts
and your subreddit list file to that new directory's res directory. From here, how you proceed
is dependent on what data you want to extract from the posts you got earlier. For example,
if you want to extract links, you can use regular expressions to get the links from the
text of the submission. For the purposes of counting, you will need to install tldextract via pip.
This module will pull the domain out of the url (for example: youtube out of https://youtube.com). We
also use requests here to expand urls in the event we find shortened urls.

```python
from collections import Counter
import json
import requests
import re
import tldextract

def do_compute():
  subreddit_list = []
  counts = Counter()
  with open("your_list.json", "r") as sub_list:
    subreddit_list = json.load(sub_list)
  for sub in subreddit_list:
    for filename in os.listdir(os.path.join(os.getcwd(), sub)):
      cur_post = None
      text = None
      with open(filename, "r") as post_read:
        cur_post = json.load(post_read)
      if cur_post is not None:
        if cur_post["is_self"] == True:
          text = cur_post["selftext"]
        else:
          text = cur_post["url"]
        found_urls = re.findall(r"https?://\S", text) # Find links in the post text using regular expressions
        for url in found_urls:
          expanded_url = requests.get(url).url
          domain = tldextract.extract(expanded_url).domain
          counts[domain] += 1
  with open("res/counts.json", "w") as fout:
    s = json.dumps(counts, indent=4)
    fout.write(s)
```

And with that, we have successfully gotten the desired data and counted it. We can now move on to
creating a visualization of our findings.
