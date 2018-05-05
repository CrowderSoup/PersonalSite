+++
title = "Using Husky to Build Hugo Site"
description = "Using Husky to ensure that hugo is run to generate site on commit"
date = "2018-05-05 16:30:00"
categories = ["Site Updates"]
tags = [
    "huskyjs",
    "node",
    "npm",
    "git",
    "hugo"
]
+++
I've been making some efforts to streamline the publishing process for this
site. I've read about tools like [Netlify][1] and [Lektor][2], but I wanted to
keep things as close to a basic [Hugo][3] site as possible.

To that end, I wanted to use git hooks to run hugo whenever I ran `git commit`.
That way to publish a new post I simply had to write it in markdown, save,
commit and push. No remembering to run hugo. No remembering to add changes to
the site. A plain and simple git workflow for publishing.

I have seen [husky][4] before and decided to give that a go for this project.
It's an npm package that allows you to define your git hooks in your
`package.json`, which will make it easy for me to maintain the hooks I want to
use.

To get started I first had to initialize my `package.json` file:

```
npm init
```

Then I installed husky:

```
npm install husky@next --save-dev
```

And finally update my `package.json` with the following scripts and husky
config:

```
"scripts": {
  "build": "hugo",
  "dev": "hugo server"
},
"husky": {
  "hooks": {
    "pre-commit": "npm run build && git add docs/*"
  }
}
```

Now I can use npm to run the hugo server (not that that's easier than `hugo
server`) and build the site. The real value though is that any time I commit
the build will automatically run and the resulting build will be added before
the commit.

<!--Links-->
[1]: https://www.netlifycms.org/
[2]: https://www.getlektor.com/
[3]: http://gohugo.io/
[4]: https://github.com/typicode/husky
