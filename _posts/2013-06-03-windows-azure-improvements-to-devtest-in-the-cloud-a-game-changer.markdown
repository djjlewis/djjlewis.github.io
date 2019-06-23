---
layout: post
title: 'Windows Azure Improvements to Dev/Test in the cloud: A Game Changer?'
date: '2013-06-03 19:58:49'
tags:
- azure
- development
- cloud
---

<a href="http://weblogs.asp.net/scottgu/">Scott Guthrie</a> has just posted an announcement on his blog detailing "<a href="http://weblogs.asp.net/scottgu/archive/2013/06/03/windows-azure-announcing-major-improvements-for-dev-test-in-the-cloud.aspx">Major Improvements for Dev/Test in the Cloud</a>".

I have been looking into (and actively using) more and more Windows Azure services over the last 6-12 months, especially since the pace seems to have picked up in delivering new features and improving the overall usability such as switching to the new and improved management portal. That's not to mention the fact the MS are pushing more and more with this and that it is now becoming almost impossible to ignore.

Generally speaking I am sold already and we have a number of production sites running as Azure websites.

The one scenario that has not worked so well for me to until now has been moving my day-to-day dev and test environments into Azure, for the simple reason that it was a major hassle to de-provision your VMs when you were no longer not actively using them, otherwise they still count to your hourly billing charge (yes, even when turned off!).

It's not actually that difficult to knock-up some PowerShell scripts that will export your VM configurations to disk and then re-provision them at a later date, but it was just enough of a hurdle to stop from doing this day to day.

Luckily this is no longer the case, because as outlined in Scott's blog post above, VMs that have been shutdown / turned-off no longer count to your billing charge. THIS IS FANTASTIC!!

In addition to this, it is now (legally) possible to install your MSDN software into an Azure VM, and they are also offering heavily discounted access to development VM images for things like Windows Server, SQL Server, and BizTalk.

All in all, I think this is going to be a real game-changer for those developers (myself included) who have been considering moving their development environments into the cloud but were put off by cost and barriers to entry.

Kudos to Scott Guthrie and the Azure team, and please continue to keep up the excellent work...