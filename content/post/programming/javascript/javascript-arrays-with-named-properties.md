+++
title = "JavaScript: Array's with named Properties"
date = "2015-11-11 12:46:49"
categories = ["JavaScript"]
tags = [
    "programming",
    "javascript",
    "front-end",
    "tips"
]
+++

Adding named properties to arrays in JavaScript can be handy in a few different
cases. For instance:

- You need a nice formatted title / description for a data set. Rather than
having multiple objects you can use named properties and get away with only
using one.
- You want to add some functions to an array for whatever reason
- Lots of other reasons that I can't think of right now!

Basically, this just buys you a nice way to encapsulate all the data you might
need, without having to use an object with a nested array, or multiple objects.
Maybe your way is more clean or better for this reason or that... I just
thought this was neat. :)

Let's get into some code to play around with this. I'm going to use
[JSFiddle.net](https://jsfiddle.net) for this so you can play with the code
yourself.

<iframe width="100%" height="300" src="//jsfiddle.net/CrowderSoup/b41q0hc6/8/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

The reason that this works is because of the way that `array.length` is
updated. In JavaScript, `array.length` is updated whenever you use a built-in
array method (e.g., join, push, unshift, etc). So, when you build an array,
all the numerically indexed properties are taken into accound as part of the
length.

When you add a named property to the array it doesn't update the length, and
therefore you can iterate over an array and only get the numerically indexed
items.
