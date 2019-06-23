---
layout: post
title: DVWP / DFWP properties cleared / "An error occurred processing the data view.
  The XslText property is empty."
date: '2008-11-04 10:11:21'
tags:
- sharepoint
---

I was having a strange issue when adding a DataView / DataForm webpart into a webpart zone whereby it was being rendered correctly on the first page visit but then any page interactions including post-backs would cause all of the properties to be wiped. A symptom of this was the message above ("An error occurred processing the data view. The XslText property is empty.") which was caused by both the XSL and XslLink properties being cleared, but was obviously not the root cause. The only other clue I was getting was an error about "An error occurred while parsing <em></em>EntityName. Line X, Position Y". This led me to believe it was a problem with the DataView transforming the XML via the XSL template.

After much investigation and comparing the erroneous webpart to a working one, I found that the issue is caused when you have a column / field in the DataFields element of the DataView with an ampersand (&amp;) character - even though it is escaped properly e.g.

&lt;property name="DataFields" type="string"&gt;@ID,ID;@ContentType,Content Type; ... @ThisAndThat, This &amp;amp; That; ... &lt;/property&gt;

Changing the above line to :

&lt;property name="DataFields" type="string"&gt;@ID,ID;@ContentType,Content Type; ... @ThisAndThat, This and That; ... &lt;/property&gt;

cured the problem. If you still want the ampersand displayed in the form, then you need to change it in the xsl directly. Obviously ampersands are not supported in the column display name of the datasources element, which seems amazing that I haven't encountered this before.