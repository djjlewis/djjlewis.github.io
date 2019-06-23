---
layout: post
title: The base type 'System.Web.UI.MasterPage' is not allowed for this page
date: '2008-09-10 15:05:49'
tags:
- sharepoint
---

I've been using the telerik controls in a custom SharePoint application and decided to go with the latest .NET 3.5 ajax implementation. There are already a couple of ways to add ASP.NET Ajax support to WSS/MOSS including the "official" way here (requires SP1): <a href="http://msdn.microsoft.com/en-us/library/bb861898.aspx">http://msdn.microsoft.com/en-us/library/bb861898.aspx</a> which uses the original ASP.NET Ajax released for .NET 2.0 / VS 2005.

To enable .NET 3.5 on my SharePoint web app, I used the 3.5 config feature provided as part of the SharePoint features set on CodePlex: <a href="http://www.codeplex.com/features">http://www.codeplex.com/features</a> which was started by <a href="http://scothillier.spaces.live.com/blog/">Scott Hillier</a>.

One oddity I came across after doing this, was that if I customised (unghosted) my masterpage in SharePoint Designer  (which contains the ScriptManager control), none of my content pages would load and would throw an exception along the lines of: "The base type 'System.Web.UI.MasterPage' is not allowed for this page".

After doing some digging in the web.config and comparing entries to the eralier "official" guidance, I notcied I had an extra control tag entry in the web.config:
<pre>&lt;add tagPrefix="asp" namespace="System.Web.UI.WebControls" assembly="System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31BF3856AD364E35" /&gt;</pre>
After removing this entry my content pages now load fine when the masterpage had been customised. I have yet to see if there are any other side effects to this, but I'll do a follow up post if I find anything more.