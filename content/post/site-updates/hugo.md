+++
title = "Moving to Hugo"
description = "an adventure moving from Pelican to Hugo"
date = "2017-11-29 23:41:08"
categories = ["Site Updates"]
tags = [
    "go",
    "hugo",
    "pelican",
    "python"
]
thumbnail = ""
+++

Last night I got the wild hare to migrate my personal site from [Pelican][1] to
[Hugo][2]. I've been meaning to do it for a while now, so to give myself the
push I needed to get it done I *deleted* my old personal site from [Github][3].

### Differences

#### Front Matter
Honestly the biggest different for content is "front matter". Both Hugo and
Pelican, as static site generators, use front matter to describe pieces of
content.

Front matter for Pelican might look something like this:

```markdown
Title: Blog Post Title
Date: 2017-11-29 23:51:34
```

Whereas Hugo's would look like this:
```markdown
+++
title = "Blog Post Title"
date = "2017-11-29 23:51:34"
+++
```

As you can see it's pretty similar. I don't have too many posts on my blog so
it was easy to go through and manually update each one. If I had more posts
I probably would have written a script to make the conversion for me.

#### Fold Structure
This likely doesn't come as a surprise, but just as the front matter format
isn't compatible neither is the project fold structure. Pelican keeps everything
you're going to render under the `content` folder. Under that content folder you
have folders for posts, pages, and static content. Something like this:

```
- content
    - posts
        - welcome.md
    - pages
        - about.md
    - assets
        - style.css
```

Hugo likes to keep only real **content** under the `content` folder. Hugo also
makes no assumptions about the TYPE of content your site will have. Each file
represents a node in your site-map. How those nodes are rendered as your site
is up to your theme!

Hugo does allow for static content though. It lives, simply, under the `static`
folder at the root of your site. For me, this meant copying not only the actual
content from `content/posts` and `content/pages` just Hugo's `content` folder,
but also moving `content/assets` to `static` in Hugo.

#### Themes
One of the things that drew me to Hugo was how powerful a Hugo theme is. As
I said before, a Hugo theme actually dictates the structure in which your
content will be rendered. A theme can describe a set of default layouts for
list pages, single pages, etc. It can also override the layout of any
individual page.

Hugo themes can be as simple or verbose as you choose. Pelican themes require
more files, and generally seemed less flexible to me. Though, this may have
been due simply to my own implementation.

### Hugo's advantages
#### Speed
Purely anecdotal, but Hugo feels **much** faster than Pelican. This site (while
small) builds in less than 20ms. It's not so much that Pelican was **slow**,
it's just that Hugo is **so** much faster.

#### Flexibility
Hugo has baked in i18n support. It has support for building multiple content
types (JSON, AMP, etc.). It supports whatever taxonomies, content types, and
menus you can dream up. A number of shortcodes are baked in and ready to use in
your markdown, and you can write as many custom ones as you want.

Bottom line, I've found Hugo to be far more flexible than Pelican.

### Other Non Hugo Vs Pelican Changes
One of the biggest changes I've made to this site is that it's now run out of
a single git repository hosted on [Github][3]. Github now let's you host
a repositories "Github Pages" site out of a subfolder instead of the root of
the repo or a special "gh-pages" branch. This is not without caveats though:

1. The repo cannot follow the "username.github.io" or "project.github.io"
   naming scheme.
2. The subfolder **must** be named `docs`, not `public` which is what hugo
   renders to by default.

These are both easily solvable problems. Name your repo something like
"Personal-Site" and set `publishDir = "docs"` in your config.toml. I used
a custom domain for my site as well so I really don't care what the repo is
called because the URL is whatever I set in the `CNAME` file in the repo root.

[You can check out the repo for this site here][4]

### Disclaimer
Okay, so if you've made it this far you may be thinking to yourself "Hey, this
guy didn't include any **actual** data to back up his claims!". And that's on
purpose. I tested and used Pelican extensively myself and decided I like Hugo
better. But anyone can fake benchmarks. That's why I think they're rubbish.
Pelican may be the right choice for you, which is why I encourage you to give
it a go! I picked Hugo in the end, but you may not!

<!-- Links -->
[1]: https://github.com/getpelican/pelican
[2]: https://gohugo.io
[3]: https://github.com
[4]: https://github.com/crowdersoup/PersonalSite
