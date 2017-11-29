+++
title = "New Theme!"
date = "2016-01-06 16:30:00"
categories = ["Site Updates"]
tags = [
    "update",
    "front-end",
    "pelican"
]
+++

I recently started using [Pelican](1) static site generator for this blog. I was
drawn to it for a few reasons:

1. It uses [Jinja2](2) for templates, which I love.
2. It written in python
3. It reminds me a lot of [Flask](3) (this might be because of using Jinja2...)

I've done a few interesting things with this site though. I'm hosting the repo
that contains the source content, configuration, etc. on [Gitlab](4). I
initially thought I'd host this site using Gitlab's new "Pages" feature, but it
wasn't quite up to snuff yet. For one, the "build" process was REALLY slow. For
two, you couldn't use a custom domain.

Instead, I decided to host the site out of a [Github](5) repository. Github
Pages deploy in seconds and they allow me to use a custom domain for my site. I
actually use [Make](6) to build the site locally during testing as well as
"publishing" it to my Github repository. This means that the site and it's
content are replicated to two different locations on two different services so
my data and content are as safe as possible (from things like accidental deletions,
services shutting down and the like).

### Custom Theme
I wanted to build my own theme for Pelican rather than using one from their
[Theme Repository](7). I felt like I could build something in a fairly short
amount of time that would best match my tastes and how I wanted my site and
content to come across.

It took me a few days working here and there, but what you're looking at now is
my new custom theme!

#### Process
Building a Pelican theme was actually a fairly straightforward process.
Especially compared to some of the CMSs I've built themes for in the past
(*cough* WordPress *cough*). [Their guide](8) gives you a list of files you'll
need, along with all the different variables and configuration options available
to you.

As I mentioned before, Pelican uses Jinja2. All the template files are written
using it. The theme documentation gives you an idea of what each theme file
should contain or look like. In a few cases I looked at what some other themes
where doing from the [Theme Repo](7). Those two resources combined gave me the
tools I needed to get building.

#### PersonalSite-theme
This theme, lovingly called "PersonalSite-theme" (or coldly, can never remember
which it is), uses a couple of fun technologies to improve the development
process.

**NPM**
I'm using NPM to install various JavaScript packages. A lot of folks combine
NPM and [Bower](9), using NPM for cli tools, and Bower for client-side JavaScript
Libraries (like jQuery, Bootstrap, etc). I decided to **just** use NPM, as they've
fixed a lot of the issues that made using Bower a requirement.

I use NPM to install:
- [Gulp](10), a task runner.
- [Gulp-Sass](14), a tool that let's me compile [Sass](15) using Gulp.
- [Bootstrap](11), a client-side UI framework. Provides CSS styles and JavaScript
UI components that make building a clean / beautiful UI somewhat trivial.
- [jQuery](12), we all know it. Some of us love it, some hate it. I needed it.
- [Font Awesome](13), a font icon library.

**Gulp**
Gulp is a really important tool that I used in my workflow for developing this
theme. After using NPM to install packages I then used Gulp to to move things
from the `node_modules` directory that they're downloaded to into the `static`
folder of the theme. Gulp was also responsible for watching my `*.sass` file for
changes and running the compiler.

These tools combined really streamlined my workflow and made development a
breeze. Before this project I had used NPM, but not Gulp. I *had* used another
task runner, but Gulp was by far the best one I've used.

#### Usage
So, you want to use this theme for your own Pelican site? Well, it's REALLY easy.
You must first have [NodeJS](https://nodejs.org/en/) installed, which
comes with `npm`, a package management tool. Once you have that you can clone
the repository to where ever you keep your Pelican themes (I personally put them
as submodules of my Pelican sites repo, but that's a topic for another post) and
run `npm install && gulp` at the root of the theme repo.

### Wrapping up
I hope you enjoyed this post and learning more about Pelican and my sites theme
in general. If you have any specific questions about this theme or it's usage
let me know in the comments or [on Twitter](16).

[1]: http://getpelican.com "Get Pelican"
[2]: http://jinja.pocoo.org/ "Jinja2"
[3]: http://flask.pocoo.org/ "Flask"
[4]: https://gitlab.com/crowdersoup/crowdersoup.gitlab.io "Gitlab Repo"
[5]: https://github.com/CrowderSoup/crowdersoup.github.io "Github Repo"
[6]: https://www.gnu.org/software/make/ "Make"
[7]: https://github.com/getpelican/pelican-themes "Pelican Theme Repository"
[8]: http://docs.getpelican.com/en/3.6.3/themes.html "Pelican Theme Documentation"
[9]: http://bower.io/ "Bower, Client-side packages"
[10]: http://gulpjs.com/ "Gulp, a task runner"
[11]: http://getbootstrap.com "Bootstrap"
[12]: https://jquery.com/ "jQuery"
[13]: http://fontawesome.io/ "Font Awesome"
[14]: https://www.npmjs.com/package/gulp-sass "Gulp-Sass"
[15]: http://sass-lang.com/ "Sass"
[16]: http://twitter.com/crowdersoup "&amp;CrowderSoup"
