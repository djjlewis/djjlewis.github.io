---
layout: post
title: Solving 'The iTunes Store is temporarily unavailable. Please try again later.'
  on Mac OS X
date: '2015-07-09 12:31:04'
---

**TL;DR**: Try "De-authorize this computer" and then "Authorize this computer" from the Account menu.

I did a clean install of Yosemite on my mid-2012 rMBP a few weeks ago, as I had upgraded from Mountain Lion to Mavericks to Yosemite and there was now a bit more cruft hanging around then I would have liked. To be fair, this was the first time since it was new in 2012, which is saying something compared to previous OSs I have used in the past!

One side-effect was that iTunes refused to launch from the dock (but could from the command line) and I ended up using a suggestion I found online that involved completely removing iTunes and it's user / library data with sudo, and then downloading and re-installing it.

All was good, or so I thought, until yesterday when I tried to make a purchase through the iTunes store and was consistently greeted with the  message "The iTunes Store is temporarily unavailable. Please try again later."

It seems iTunes 12 can no longer be easily removed from Yosemite, so out went that plan, and after a reboot and still no joy I was at a dead end.

Having remembered my previous uninstall / re-install, I wondered if my account / computer authorisation was messed up so I went to the Account Menu, chose "De-authorize This Computer" and then immediately followed with a "Authorize This Computer" and sure enough the purchase worked immediately!
