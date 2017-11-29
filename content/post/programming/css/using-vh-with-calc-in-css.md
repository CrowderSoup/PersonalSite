+++
title = "Using vh with calc In CSS"
date = "2015-11-17 09:45:00"
categories = ["CSS"]
tags = [
    "programming",
    "css",
    "front-end",
    "design"
]
+++

I often have need to build layout's that vary depending on the content put in
them. I can't always count on that content being the same (*cough* CMSs *cough*).
It's just one of those things you have to do.

One thing I'm having to do a lot though, is making the body of a page take up a
certain amount of space so that the footer doesn't look weird. In the past I've
used JavaScript to make the footer take up the remaining space on the page if the
content didn't take up enough. I never really liked that solution though, because
it breaks if the user turns off JavaScript.

Today I wanted to share with you two CSS things, that when combined solve my
particular problem, and might just solve yours too.

### vh

>Equal to 1% of the height of the initial containing block.

*from [w3.org](http://www.w3.org/TR/css3-values/#viewport-relative-lengths)*

This gives us the **height** of the page, which we're going to need to calculate
how much space the main content area of the page should take up.

### clac

> With `calc()`, you can perform calculations to determine CSS property values.

*from [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/calc)*

This allows us to perform mathematical calculations and set a property to the
result. This, combined with `vh` gives us a lot of power!

### My Solution

In order to ensure that the body of a site I'm working on is always taking up *at
least* enough to completely fill the page. I have a couple of things on the page
that are fixed height (header and footer). I take the aggregate height of them
and subtract that from `100vh` (100% of the viewport height), like so:

```css
#body {
    min-height: calc(100vh - 405px);
}
```

Now `#body` is going to be *at least* the height of `100vh - 405px`!

This is just one use-case. I'm sure there are tons of others! What are you using
`calc` and `vh` for in your projects?
