---
layout: post
title: Cisco IP Communicator 7 on Windows 7 x64 only uses Default Audio device
date: '2010-11-18 12:11:32'
---

<p>I use the <a href="http://www.cisco.com/en/US/products/sw/voicesw/ps5475/index.html">Cisco IP Communicator</a> soft-phone when working from home, and although I am able to run version 7.0.2.0 on Windows 7 x64 (using WoW64) I have had a very annoying issue whereby it will only display the default windows audio device as an option when going through the audio tuning wizard. This means that I have had to set my Plantronics CS60 hands-free usb headset as the default Windows audio device (rather than just the default communications device) which has the knock-on effect of playing all Windows sound through the headset – very annoying!</p>  <p>Luckily, after a quick Google of the issue, I found <a href="http://social.technet.microsoft.com/Forums/en/w7itproappcompat/thread/a8745d05-a369-453d-b967-5ad827fff079">a post that suggested setting the compatibility mode for the communicator app to Vista SP2</a>. I have since done this and can confirm that the USB headset is no listed as a separate option in the audio wizard dialogs – huzzah!</p>