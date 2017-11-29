+++
title = "Anatomy of a Commit Message"
date = "2015-11-13 07:15:33"
categories = ["Programming"]
tags = [
    "programming",
    "git"
]
+++

## 1. Subject Line
The Subject Line is the first line of your commit message. Often the subject
alone is enough, but if it's not and you need a body be sure to separate the
subject and body with a blank line.

- First line of a commit message
- Often the only part you'll need
- Separated from the body by a blank line
- Soft limit of 50 characters, hard limit of 69
    - Github's interface truncates the subject line at 69 characters
- Capitalize!
- Don't end with a period
- Use the imperative mood
    - Git itself uses the imperative mood when it creates a commit on your behalf
    - We usually write in the indicative mood, which is more about reporting facts
    - To help, the subject line should always complete the sentence:
        - "If applied, this commit will..."


## 2. Body
- Wrap the body at 72 characters
    - This give git plenty of room to indent text while still keeping things
    under 80 characters.
- Use the body to explain what and why vs. how
    - The code tells us the *how*, the body of your commit message should tell us
    *what* and *why*.


## Sample Commit Messages

**Bad**
```
Fixed the thing
```

**Good**
```
Fix all the broken things

There were some broken things so I refactored many codes to simplify
and fix all the things.
```

- Uses the imperative mood for the subject line
- Separates the subject from the body with a single blank line
- Describes the what and why in the body
