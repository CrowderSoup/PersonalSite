# CrowderSoup.com

This is my personal site, hosted at [crowdersoup.com](http://crowdersoup.com).
It is hosted using Github Pages **for free**. Can't beat free!

This site uses:

- [Hugo](http://gohugo.io)
- [Basics Plus](https://github.com/crowdersoup/basics-plus)

I have Hugo configured to publish to the `docs` folder to allow me to host this
site out of a single repository. This way I can have the published content and
the source all in one place on Github. This makes publishing MUCH easier.

I'm using [Husky](https://www.npmjs.com/package/husky) (an NPM package) to
easily configure git hooks. I have two tasks in my `package.json`, one for
running the hugo dev server, and other other being to generate the site as
a pre-commit hook. This enables me to publish the site by simply committing and
pushing this repo.
