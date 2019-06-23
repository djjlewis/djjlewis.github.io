---
layout: post
title: Error setting SharePoint property
date: '2009-12-11 11:09:53'
---

I recently went to update a property on my development SharePoint server (peoplepicker-onlysearchsitecollection as it happens) and after typing in the full stsadm –o setproperty command was greeted with this rather worrying message:

<em>“The server administration programs and the Windows SharePoint Services Web applications on this Web server are not compatible.  Ensure that the administration program is the same version as the Web application.”</em>

My initial reaction was that somehow a recent hotfix had failed to apply correctly and different components were now running different versions – arghh!

Fortunately that turned out not be the case and the answer was very simple – the url parameter I had used for the SharePoint site was not correct. After putting in the correct URL, it ran perfectly, although it certainly was not the most obvious answer given the message above!