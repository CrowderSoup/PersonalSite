+++
title = "Raspberry Pi Zero Giveaway: Review"
date = "2016-01-13 09:00:00"
categories = ["Raspberry Pi"]
tags = [
    "raspberry pi",
    "zero",
    "giveaway",
    "maker"
]
+++

I've been watching my local [Barnes & Nobel's](1) like a hawk the past few
weeks. In case you've been living under a rock, the official Raspberry Pi
magazine, [MagPi](2), shipped with the new [Raspberry Pi Zero](3) attached to
the cover.

The Raspberry Pi Zero, announced in late November of 2015, has been flying off
shelves as fast as it's stocked. They're HARD to get your hands on. I should
know, I've been trying since they were first announced! I knew my best bet would
be to get a copy of the MagPi when it finally shipped to the States.

When first announced, lots of folks started buying up the stock of Zero's and
selling them at jacked-up prices. The Raspberry Pi foundation urged buyers not
to encourage price gougers, and to wait for more inventory. I decided to follow
this request as I felt that price gougers were going against the spirit of
the Pi itself. Computers should be evenly distributed at an affordable price to
all people.

However, I started to realize that the distribution of Zero's (and the MagPi)
were pretty uneven. Places that didn't need as much stock, got more than needed,
places that needed more didn't get enough. This led to people starting to buy
them for other folks, as well as giveaways to try and get these tiny computers
into as many hands as possible.

That's why I posted in the [Raspberry Pi Subreddit](4) on Monday. I was FINALLY
able to get my hands on the coveted Issue #40 of the MagPi. Not only was I able
to get **one**, but due to the uneven distribution that I talked about, my local
Barnes & Nobel had plenty of stock, and I was able to get a **second**. I
wanted to be able to give a Zero to someone who hasn't been able to find one
yet. Someone who would build something truly *awesome* with it.

Before I talk about the results of the giveaway, I want to talk about the
technology behind it. I decided to use a simple python script to automate
gathering contest entries from the Reddit Post. I could then, again with python,
select a random winner.

### [The Code](5)
I put all the code up on Github so that no issues would arise with claims of
unfairness. I also wanted to write the code in such a way that I could
easily repurpose it for another giveaway in the future (by either myself or
anyone else willing to fork the repo).

I used [PRAW](6) to gather the data from the Reddit Post. It was pretty trivial
to provide PRAW with a Submission ID and then loop over all the comments. Here's
what I did:

```python
# We connect to Reddit using a Unique user_agent
r = praw.Reddit(user_agent='Reddit Raspberry Pi Giveaway (by /u/IrishLadd)')

# We get the submission, "SUBMISSION" here comes from a config file
submission = r.get_submission(submission_id=SUBMISSION)

# Let's make sure we get ALL comments in the thread:
submission.replace_more_comments(limit=None, threshold=0)

for comment in submission.comments:
    # Here I just did some checks to see if the comment matched, and that it's
    # author wasn't already on the list of entries.
```

Like I said, the code for this really is pretty trivial. It does, as I said
before, remove any doubt that it was a fair contest. After getting all the
entries I then count the total number, and get a random `int` from 1 to that
number. This is the winning line!

```python
entry_count = 0
with open("entries.csv", "r") as entries:
    entry_count = sum(1 for _ in entries) - 1

winning_entry_number = random.randint(1, entry_count)
winning_entry = linecache.getline('entries.csv', winning_entry_number)
winning_entry_parts = winning_entry.split(',')
winning_user = winning_entry_parts[0].strip(' "\'\t\r\n')
winning_permalink = winning_entry_parts[1].strip(' "\'\t\r\n')
```

So, without further adieu...

### The Winner!

The winner is [/u/nullandkale](http://reddit.com/u/nullandkale), with
[their entry](https://www.reddit.com/r/raspberry_pi/comments/40idxl/another_raspberry_pi_0_giveaway/cyushol)
of:

> I would build either a controller to auto turn my computer off when I left the
> house, or some sort of retropi handheld.

Here's the script spitting out the results:

![Results](http://i.imgur.com/cwi9q4m.png)

Thanks to everyone who played!

[1]: http:// "Barnes & Nobel"
[2]: http:// "The MagPi"
[3]: http:// "Raspberry Pi Zero"
[4]: http:// "Raspberry Pi Subreddit"
[5]: http:// "Github Repo, Reddit Giveaway"
[6]: https://praw.readthedocs.org/en/stable/ "Python Reddit API Wrapper"
