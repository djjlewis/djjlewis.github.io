---
layout: post
title: How to fix “Input string was not in a correct format” when using calculated
  date columns in a SharePoint / WSS list calendar view
date: '2010-11-10 22:51:39'
---

<p>When I recently tried to create a new SharePoint / WSS calendar view on a list that uses calculated columns for the both the start and end dates, I was greeted with the following error message:”Input string was not in a correct format”</p>  <p>After quite a bit of trawling the web (hence this blog post), it seemed to be a known issue in certain version of SharePoint / WSS. This particular server was already at SP2 (12.0.0.6421) so I decided to go ahead and install the latest CU - currently August 2010 (12.0.0.6545).</p>  <p>After installing the CU, rebooting and running through the farm configuration wizard, I recreated the calendar view and this time everything worked perfectly.</p>  <p>Here’s a handy reference to the available <a href="http://www.sharepointdevwiki.com/display/SharePointAdministrationWiki/SharePoint+Versions">SharePoint hotfixes and version numbers</a>.</p>