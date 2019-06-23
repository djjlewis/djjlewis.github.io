---
layout: post
title: "“Feature '{guid}' is not activated at this scope.” when retracting a SharePoint
  solution package in Visual Studio 2010"
date: '2011-03-17 18:38:11'
---

<p>I was consistently getting the message “Feature '{guid}' is not activated at this scope.” when retracting a particular SharePoint 2010 solution developed and deployed via the new(ish) Visual Studio 2010 SharePoint Developer tools.</p>  <p>After a very quick test it seems to be caused when you have a feature that is itself dependent on another hidden.</p>  <p>In this case, when solution is deployed and the first (visible) feature is activated, SharePoint will automatically activate the dependent hidden feature.</p>  <p>However, when retracting the solution, the error reported above is (I believe) caused because Visual Studio will deactivate the first (visible) feature, but then SharePoint kicks in and deactivates the dependent (hidden) and then, when Visual Studio tries to deactivate the dependent feature it has of course already been disabled.</p>  <p>All in all then, nothing to worry about – just slightly annoying that you are forced to see (and worry about) the message!</p>