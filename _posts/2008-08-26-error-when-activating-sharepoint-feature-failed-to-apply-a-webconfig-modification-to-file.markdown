---
layout: post
title: 'Error when activating SharePoint Feature: Failed to apply a web.config modification
  to file'
date: '2008-08-26 14:39:57'
tags:
- sharepoint
---

I had trouble activating a SharePoint feature on my site which was causing the following error:
<pre>Failed to apply a web.config modification to file 'configuration/system.web/page
s'.  The specified node "C:InetpubwwwrootwssVirtualDirectories80web.co
nfig" was not found in the web.config file.</pre>
While at first quite confusing, it turns out that that the error message was indeed correct ;-)... after I compared it with an earlier web.config the entire &lt;pages&gt; section had been removed (maybe by a previous rogue feature receiver?), so I re-added the following lines, and hey presto all was fine:
<pre style="padding-left:30px;">&lt;pages enableSessionState="false" enableViewState="true" enableViewStateMac="true" validateRequest="false" pageParserFilterType="Microsoft.SharePoint.ApplicationRuntime.SPPageParserFilter, Microsoft.SharePoint, Version=12.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" asyncTimeout="7"&gt;
&lt;namespaces&gt;
&lt;remove namespace="System.Web.UI.WebControls.WebParts" /&gt;
&lt;/namespaces&gt;
&lt;tagMapping&gt;
&lt;add tagType="System.Web.UI.WebControls.SqlDataSource, System.Web, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" mappedTagType="Microsoft.SharePoint.WebControls.SPSqlDataSource, Microsoft.SharePoint, Version=12.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" /&gt;
&lt;/tagMapping&gt;
&lt;/pages&gt;</pre>
Dan.