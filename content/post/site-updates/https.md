+++
title = "GitHub Pages Over HTTPS"
description = "Using HTTPS for sites with custom domains on GitHub Pages"
date = "2018-05-05 11:45:00"
categories = ["Site Updates"]
tags = [
    "security",
    "https"
]
+++
Using HTTPS for your site has lots of benefits. Chief among them being
security. Using HTTPS ensures that no one can intercept and read traffic
between you and the site you're visiting.

However, it's traditionally been somewhat difficult and expensive to provide
HTTPS for your sites visitors. Now though, with [Let's Encrypt][1] an SSL
certificate is free! And if you're using GitHub pages with a custom domain for
hosting using it couldn't be easier.

All you have to do is [set up your custom domain][2] to point to your GitHub pages
site, and then update the settings on your repo to look like mine:

![GitHub Pages Settings](/assets/uploads/2018/05/GitHubPagesHTTPSConfig.png)

If, like me, you're already using a custom domain on GitHub pages then you have
to follow these simple steps to enable HTTPS:

1. Remove your custom domain and save
2. Re-add your custom domain and save again
3. The "Enforce HTTPS" checkbox should now be enabled

Now you really don't have an excuse to NOT be using HTTPS!

<!--Links-->
[1]: https://letsencrypt.org/
[2]: https://help.github.com/articles/setting-up-an-apex-domain/
