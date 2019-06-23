---
layout: post
title: CTRL+F5 not working in a Windows VM running on Parallels
date: '2015-07-01 11:48:41'
---

I'm not sure if there was a change in Mac OS X between Mavericks and Yosemite, via a recent update, or possibly since I clean installed my Mac a few weeks ago, but I have had a very annoying issue recently whereby the CTRL+F5 key combination was not being picked up by my Windows 8.1 VM running in Parallels. As a developer, this was highly annoying in a couple of regular scenarios:

1. Start without Debugging in Visual Studio
2. Forcing a full refresh in a web browser window

It finally got too much today, and after a few fruitless searches on the internet I went digging in the Parallels and Mac OS settings to see if I could find the culprit. 

It turns out to be a Mac OS setting, specifically in Keyboard Settings, Shortcuts, Keyboard, and the option "Move focus to the window toolbar" which, yes you guessed it, is mapped to CTRL+F5 by default.

![Mac OS Keyboard Settings](/content/images/2015/07/Screen-Shot-2015-07-01-at-13-37-00.png)

Once this was disabled, it started being picked up in my VM once again!

As I said, this was working fine previously, so I am not sure if I had disabled this before and forgotten, but for anyone else with the same problem, hopefully this will save you some time.

A couple of related settings which are essential for using Visual Studio inside a parallels VM and which I was aware of already are [setting the function keys on your Mac to behave as function keys by default](http://kb.parallels.com/en/5020), and [making sure function keys F9-F12 are not mapped in the Mac keyboard settings](http://kb.parallels.com/en/5020) 



