+++
title = "Managing Scope Using Call, Apply, and Bind"
date = "2015-11-16 13:20:08"
categories = ["JavaScript"]
tags = [
    "programming",
    "javascript",
    "front-end",
    "tips"
]
+++

## [Call](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)

**Calls a function, with the specified arguments passed in**

The first argument becomes `this`, the rest are passed in as regular arguments.
Using call allows you to maintain the scope of `this` accross methods. It works
like this:

<iframe width="100%" height="300" src="//jsfiddle.net/CrowderSoup/xoyf7xt4/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

Here we're using prototypical inheritance to allow us to inheirit properties from
`Animal` in `Dog` and `Cat`. Using `call` allows us to invoke `Animal` to initialize
it's properties while maintaining the correct scope.


## [Apply](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)
**Calls a function, with the specified arguments passed in as an array**

Just like `call`, the first argument becomes `this`. The rest of the args are
passed in as an array.



## [Bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
**Creates a bound function with the same function body as the function it's called
on**

With `bind`, we actually get a reference to a new function. The first argument
passed to `bind` becomes `this`, and the rest are passed as regular arguments.
This is especially handy for event handlers.

<iframe width="100%" height="300" src="//jsfiddle.net/CrowderSoup/oas0LLhe/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

## Wrapping up

These examples are fairly trivial, but they do serve to show that it's possible
to manage scope without aliasing `this` to something like `self`. In a lot of
cases that can actually be pretty confusing. But, as with everything, use what
makes sense! This method may or may not work well for you, and that's okay.
