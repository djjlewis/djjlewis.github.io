---
layout: post
title: 'VSeWSS 1.3 March CTP - Error: System.ArgumentNullException'
date: '2009-06-26 11:37:42'
---

I've been using VSeWSS 1.3 recently for SharePoint development and it showed the following error message when trying to render the WSP view:

Error: System.ArgumentNullException
Value cannot be null
Parameter name: path2

Luckily the dialog also tells you where the log file is written to (AppDataRoamingMicrosoftVSeWSS1.3) so having had a look it was failing on a call to Path.Combine whereby the second parameter to combine was null (path2)

Having just added a new module to hold some custom pages this was the likely culprit and a quick "Exclude from project" in Visual Studio confirmed this.

It turns out that File element under the Module requires both the Path and Url attributes to be set. I had copied these over from an existing WSPBuilder project so it seems WSPBuilder (or more likely SharePoint) is not bothered about the Path element being set if the file is in the same location as the elements file, but clearly VSeWSS assumes this attribute is present to render out the WSP View.