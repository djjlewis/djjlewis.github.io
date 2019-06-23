---
layout: post
title: 'Installing VMWare Workstation 7 on Windows Server 2008 R2 - “Error: This product
  can only be installed on Windows XP or later.”'
date: '2009-12-04 20:27:25'
---

If you get this error message when trying to install VMWare Workstation 7 on Windows Server 2008 R2, it is most probably because you have the Hyper-V role installed and enabled which is not compatible with VMWare.

The easiest option is to follow the instructions detailed on <a href="http://blog.tiensivu.com/aaron/archives/1707-Get-power-management-features-back-with-Server-2008-Hyper-V.html">this blog</a> to disable the Hyper-V service from a command prompt and then reboot:

<em>sc config hvboot start= disabled</em>

<span style="text-decoration:line-through;">To re-enable Hyper-V, type this from a command prompt and reboot:</span>

<span style="text-decoration:line-through;"><em>sc config hvboot start= boot</em></span>

<strong>UPDATE</strong><em><strong>: </strong>It turns</em><strong> </strong><em>out you can't simply re-enable hyper-v once VMWare WS installed. If you try to run the command above you will get exactly the same message from sc.exe i.e. "The parameter is incorrect". This message is displayed because of the competing hypervisors of VMWare WS and Hyper-V and only one can be running on the system at once. This probably means</em> <em>uninstalling VMWare WS if you want to get back to Hyper-V...</em>