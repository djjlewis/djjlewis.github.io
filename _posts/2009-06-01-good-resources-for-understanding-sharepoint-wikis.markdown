---
layout: post
title: Good Resources for understanding SharePoint Wikis
date: '2009-06-01 18:53:20'
tags:
- sharepoint-development
---

I've been digging deep into the inner workings of WSS / SharePoint wikis recently as I needed to create wiki pages based off of a custom template. OOTB, the default wiki library (or rather wiki page content type) is hard-coded to call _layouts/CreateWebPage.aspx which in turn uses the DOCUMENTTEMPLATESwkpstd.aspx file as the page template. At first site, this looks like a bit of a show stopper if you wanted to use a template for a single site without affecting all the wiki pages on your entire farm.

The first resource I looked to was the <a href="http://cks.codeplex.com/">Community Kit for SharePoint</a>: Enhanced Wiki Edition (CKS:EWE) which currently stands at Beta 2 and will get you pretty much there to achieve what I was after.

Having obtained what I thought was a reasonable understanding of the workings of SharePoint wikis I happened upon on a blog post by David Mann (who I believe worked on CKS:EWE) entitled <a href="http://www.mannsoftware.com/blog/archive/2008/12.aspx?PageIndex=5">"How SharePoint Wikis Work</a>". The title says it all really and is pretty much the most comprehensive and clear discussion on the technical workings of SharePoint wikis that I have come across so far. The post has certainly clarified a few things for me and also taught me a couple of new things (the existence of SPWeb.RootFolder.WelcomePage for one)- my only wish is that I had come across this great resource earlier!

With these resources I can finally start putting the finishing touches on my latest feature.