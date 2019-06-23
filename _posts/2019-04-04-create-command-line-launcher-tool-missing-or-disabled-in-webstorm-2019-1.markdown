---
layout: post
title: Create Command-Line Launcher Tool missing or disabled in WebStorm 2019.1
image: ''
date: '2019-04-04 21:41:40'
---

Having recently installed the latest and greatest WebStorm (2019.1), as is usually the case, the script generated to run from a macos terminal no longer worked as they tend to only work with a particular product version e.g. still pointing at 2018.3.4 or whatever.

I went to the Tool menu as I normally would but was surprised to find the "Create Command-Line Launcher" command was missing.

I _could_ find it in the Actions / Search Everywhere menu, but the option seemed to be disabled and did nothing when I ran it.

It turns out that this [feature is now disabled if you use the JetBrains Toolbox app](https://youtrack.jetbrains.com/issue/IDEA-206235) (which I do), and it is now responsible for generating these scripts for all your installed JetBrains products. Sounds nice in theory ... if it works!

I opened the Toolbox app, went to settings, ensured Generate shell scripts was enabled, and added a location in the path (I chose `/usr/local/bin` that the scripts would previously have been created in), then quit and restart the Toolbox app, and all seems to be good in the world one more!

![](/content/images/2019/04/Screenshot-2019-04-04-at-22.32.51.png) 

 