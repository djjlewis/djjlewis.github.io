---
layout: post
title: A quick way to check if a sub site exists using the SharePoint 2013 .NET Client
  Side Object Model (CSOM)
date: '2013-10-02 18:28:46'
---

As per the title of the this post, here is a very quick code sample demonstrating how to check if a sub web already exists using the .NET CSOM in SharePoint 2013 (I imagine this should work on 2010 also):


`bool WebExists(string siteUrl, string webUrl)
{
	//connect to the root site
	using (ClientContext context = new ClientContext(siteUrl))
	{
		// load up the root web object but only 
		// specifying the sub webs property to avoid 
		// unneeded network traffic
	    var web = context.Web;
    	context.Load(web, w =&gt; w.Webs);
	    context.ExecuteQuery();
    	// use a simple linq query to get any sub webs with the URL we want to check
	    var subWeb = (from w in web.Webs where w.Url == webUrl select w).SingleOrDefault();
	    if (subWeb != null)
    	{
	      // if found true
    	  return true;
    	}
  	}
  	// default to false...
  	return false;
}`


You would call this as follows:


`var siteExists = WebExists("http://host/sites/site/", "http://host/sites/site/subsite");`

