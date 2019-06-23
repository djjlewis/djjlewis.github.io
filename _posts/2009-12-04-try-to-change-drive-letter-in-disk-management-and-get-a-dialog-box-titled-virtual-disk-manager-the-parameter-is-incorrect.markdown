---
layout: post
title: Try to change drive letter in Disk Management and get a dialog box titled "Virtual
  Disk Manager" - "The parameter is Incorrect"
date: '2009-12-04 13:41:31'
tags:
- windows
---

<strong>UPDATE:<em> </em></strong><em>I was just a little too hasty posting this entry. After reading the <a href="http://technet.microsoft.com/en-us/library/dd440865%28WS.10%29.aspx">recommendations for booting from a VHD</a> on <a href="http://technet.microsoft.com">TechNet</a> it turns out that putting the page file on a physical drive rather than the virtual is required for performance reasons. In my case I just moved it to a different physical drive before changing the drive letter below.</em>

I have just setup a new Windows Server 2008 R2 installation using the new boot from VHD functionality in Windows 7 (but that's another story).

One of the things that happens is that you still get to see all of your existing drives and partitions.

I wanted to change the drive letter on my second drive, so went into "Disk Management" as usual but was surprised to see a dialog box informing me that "The parameter is incorrect" - very helpful.

After a few internet searches mainly referencing to external drives (which this is not), I suddenly spotted that the drive in question was holding the page file.

When Windows was installed, it must have chosen to put the page on this drive (whether for performance or just because there was more space available).

As it turns out, you can't change or remove a drive letter that is holding the active page file, so a quick trip through "System Properties", "Advanced", "Performance", "Advanced", "Virtual Memory", "Change..." [pause for deep breath] I moved the page file and after a quick reboot was able to change the drive letter at last.