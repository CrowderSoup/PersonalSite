+++
title = "Debugging PowerShell in VSCode"
date = "2016-04-26 09:54:00"
categories = ["Programming", "Tools"]
tags = [
    "debugging",
    "powershell",
    "scripting",
    "vscode"
]
+++

Yesterday I learned a neat trick with [Visual Studio Code](1) when working on
some PowerShell scripts to help orchestrate build and deployment of our projects
(more on that in a different post). I knew that VSCode had a debugger, but I
didn't realize that a debugger for PowerShell had been added [via an extension](0).

I had installed this extension some time ago to help with writing PowerShell
scripts in VSCode, but I was running my PowerShell prompt in another window to
actually test them. I realized that I could debug my PowerShell scripts in
VSCode so I set it up and tried it immediately. AND IT'S AWESOME.

To enable it open up a folder with you PowerShell scripts in it, go to the debug
tab, click on the gear and select "PowerShell". If you don't already have a
`.vscode/launch.json` file it will create one with the right settings. Then you
just have to open a PowerShell script, hit `F5` and away you go!

Here's the steps:

### 1. Open the Debug Tab
![Debug Tab]({{< baseurl >}}assets/uploads/2016/04/vscode_debug_tab.png)

### 2. Click the gear and select "PowerShell" from the dropdown
![Select PowerShell]({{< baseurl >}}assets/uploads/2016/04/vscode_debug_select_powershell.png)

VSCode has been awesome to work with (I'm using it to write this post!). Having
a built in debugger with a light-weight and extensible text editor has been
really cool! You can set a breakpoint really easily by clicking in the gutter to
the left of the line number (just like in any good debugging tool). Here's what
it looks like when you are actually debugging (this is actually my PowerShell
profile):

![Debugging]({{< baseurl >}}assets/uploads/2016/04/vscode_debugging.png)

What other cool things do you love about VSCode?

<!-- Links -->
[0]: https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell
[1]: https://code.visualstudio.com/
