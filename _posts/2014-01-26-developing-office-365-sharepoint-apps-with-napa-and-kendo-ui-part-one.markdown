---
layout: post
title: Developing Office 365 SharePoint Apps with Napa and Kendo UI - Part 1
date: '2014-01-26 22:22:03'
---

##Introduction
In this series of posts I am going to look at creating (and hopefully improving upon) an Office 365 SharePoint App using the Napa developer tools in tandem with some specific integration with the <a href="http://www.telerik.com/kendo-ui">Telerik Kendo UI </a>suite of HTML 5 / JavaScript web controls. I am hoping to prove (to myself at least) that it is possible to build upon the core SharePoint UI by using the SharePoint JavaScript Object Model (JSOM), in order to build modern, sleek web applications, but still keeping SharePoint as the primary backend service provider and data store.

In this first part, we will create the initial SharePoint Developer Site which will form as the basis for everything going forward. Further posts in this series will be added and linked to below as they become available. Much of the content in this series of posts will be based on my own "on the fly" experience creating this solution, so please do provide any feedback and thoughts in the comments as I go and let's learn through this process together!
##Obtaining an Office 365 Developer Site
In order to follow along you will at least need to create a new Office 365 SharePoint site based on the "Developer Site" site template. As far as I know, this is only available in the Office 365 Enterprise packages (E3 or E4), or via an Office 365 Developer subscription. If you are an MSDN subscriber, you should be able to activate a year's free Developer Subscription as part of your benefits. More info on all of this is available from the following links:

<a href="http://msdn.microsoft.com/en-us/library/office/jj692554.aspx">How to: Provision a Developer Site using your existing Office 365 subscription</a>

<a href="http://msdn.microsoft.com/en-us/library/office/fp179924.aspx">Sign up for an Office 365 Developer Site</a>

I happen to have a Developer Site subscription that I activated through my MSDN benefits, so in order to create my new Developer Site, I will navigate to my top-level SharePoint site (https://[subdomain].sharepoint.com), choose Admin then SharePoint from the global navigation, then create a new (Private) Site Collection specifying the Developer Site template. Note that you may need to specify a storage quota amount. As we will be working with relatively small JavaScript / text files, 100 -200 MB or so should easily suffice.

Once the site has provisioned, follow the link in the tenancy admin screens to navigate to the new site collection.
##Install the Napa tools app
Now that we have our Developer site set up and ready to go, it's time to install the "Napa" app. Napa allows us to develop JavaScript based SharePoint solutions completely from within a browser environment with no local tool dependencies such as Visual Studio or the like. This is perfect for quick prototyping or trying out ideas on the road when you don't have access to a full development environment, but in theory could also be used to build full production-ready apps!

To install Napa, click the Site Settings icon, then choose "Add an app". From the "Your Apps" screen click the '"Napa" Office 365 Developer Tools' and then accept any prompts about trusting the app.

![Your apps](/content/images/2014/Jan/your_apps.png)

Once Napa has finished installing, you should be able to click on the new Napa app icon that appears, which will take you to the Napa dashboard:

![Napa dashboard](/content/images/2014/Jan/napa_dashboard.png)

Click "Add New Project", select "App for SharePoint" and give the project a name e.g. KendoUISharePointApp

Once the app is created, you should see the main Napa development environment appear. In order to test the link from Napa to your Developer site is all working correctly, you can click the "Run" icon which will package and deploy your app to your developer site.

![Napa code view](/content/images/2014/Jan/napa_codeview.png)
>NOTE: If you browser tries to prevent pop-ups, you can add an allow inclusion for the www.napacloudapp.com domain.

Once deployed, follow the link to launch your app in a new window, and you should see a very basic screen showing your user name and the Page.

Congratulations! You have now created a functioning, albeit basic, Office 365 SharePoint App using the Napa development tools. In [part 2](/2014/02/01/developing-office-365-sharepoint-apps-with-napa-and-kendo-ui-part-2/), we will look to start improving on this basic project by adding a script reference to the fantastic Kendo UI HTML 5 Web controls from Telerik and adding some of the default Kendo HTML 5 widgets into our SharePoint App…