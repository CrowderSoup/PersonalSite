+++
title = "Powershell Markdown Preview"
date = "2015-10-28 00:09:20"
categories = ["Utils"]
tags = [
    "programming",
    "powershell"
]
+++

I'm at [Angle Brackets](http://anglebrackets.org). I've decided that I wanted to
try taking all my notes in vim. I LOVE using vim. It's a really awesome, powerful,
and extendable command-line editor. I enjoy that it's really distraction free.
Being distracted is something that I struggle with so I really look for ways to
stay focused.

I write in [Markdown](https://daringfireball.net/projects/markdown/) as well. It's
a great way to get a simple, clean, well formatted plain text document that can
be processed and produce HTML. One of the biggest things I look for in a Markdown
editor is being able to preview the HTML that my markdown produces. Obviously
vim isn't going to give that to me out of the box. I wouldn't expect it to either.

However, I figured I could either extend vim, or better yet, my shell to give me
markdown previews. After a bit of [Googling](https://www.google.com/webhp#newwindow=1&q=npm+cli+markdown+preview)
I was able to find an npm package called [github-markdown-preview](https://www.npmjs.com/package/github-markdown-preview).
I knew I would be able to leverage this from within vim by sending the commands
to my shell using `:shell` or even `:!`. I wanted something a little more elegant
though.

Since I'm in Windows I use PowerShell. I added the following to my PowerShell
profile:

```powershell
Set-Alias -Name gmp -Value github-markdown-preview

Function mkdown-preview($file)
{
    $preview_dir = $home + "\AppData\Local\MarkdownPreview";
    if((Test-Path $preview_dir) -eq 0) {
        New-Item -ItemType Directory -Force -Path $preview_dir;
    }

    $preview_file = $preview_dir + "\mkdown-preview.html"

    gmp $file -o $preview_file

    Start-Process "chrome.exe" "file:///C:/Users/acrowder/AppData/Local/MarkdownPreview/mkdown-preview.html"
}
```

Now I can do the following on the command line:
```bash
mkdown-preview('mkdown-file.md')
```

If the MarkDown preview folder doesn't exist then it will be created and then
we'll output the HTML generated from your Markdown to a file. Finally, we'll
open that file in Chrome for the preview. Obviously you can edit that function
to open up the browser of your choice.
