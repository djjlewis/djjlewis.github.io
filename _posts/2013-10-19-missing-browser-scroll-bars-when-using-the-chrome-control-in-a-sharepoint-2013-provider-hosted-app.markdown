---
layout: post
title: Missing browser scroll bars when using the chrome control in a SharePoint 2013  provider-hosted
  app
date: '2013-10-19 14:23:55'
---

While using the chrome control to render the SharePoint 2013 top navigation bar and gain access to the site styles in a provider hosted app, I ran into an issue whereby the browser scroll bars where not being rendered at all, making page navigation a little bit tricky!

Using the excellent Firefox developer tools and the style editor tool in particular, I was quickly able to pin-point a particular style coming through from the defaultcss.ashx handler, which the chrome control inserts into the page head in order for your app to inherit the visual styles of the SharePoint host web. 

The style in question is on line 29 (overflow:hidden) so I added an override later on in the page head e.g. [css]body { overflow: auto }[/css] and lo and behold, we have scroll bars again!