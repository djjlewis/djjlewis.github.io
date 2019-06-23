---
layout: post
title: SMTP Server no longer available to install on Windows 7
date: '2010-06-24 17:17:39'
---

<p>I picked up a useful tip over at <a href="http://stackoverflow.com">Stack Overflow</a> today while I was trying to find out how you can install the SMTP server on Windows 7 in order to test some email functionality from an ASP .NET application. </p>  <p>As it turns out you can’t as the SMTP server option is no longer available from Vista onwards. This basically leaves you with two options:</p>  <ol>   <li>Install a third party SMTP server</li>    <li>Modify the System.Net section of you web.config as detailed in this post: <a href="http://stackoverflow.com/questions/1120132/smtp-not-working-in-windows-7">SMTP not working in windows 7</a> which will redirect all smtp messages to a local folder of your choice.</li> </ol>  <p>Neat!</p>