---
layout: post
title: Updating Visual Studio 2015 RTM from ASP.NET MVC 6 beta 5 to beta 6
date: '2015-08-09 12:21:55'
---

I have been playing around more and more with the new ASP.NET 5 / MVC 6 platform now that the RTM version of Visual Studio 2015 is out. These are still in beta form and are not expected to be production ready until the end of this year, and are not slated for final release until early *next* year. 

> NOTE: The ASP.NET team recently released a [roadmap](https://github.com/aspnet/Home/wiki/Roadmap) detailing the current estimated release schedule.

In this brave new world things are certainly on a rapid release schedule, and shortly after the VS 2015 release which shipped with the ASP.NET vnext Beta 5 bits, [Beta 6 was announced](http://blogs.msdn.com/b/webdev/archive/2015/07/27/announcing-availability-of-asp-net-5-beta-6.aspx)

> The latest version of the [ASP.NET framework](https://github.com/aspnet/home) is being built completely in the open on GitHub so you can see commits coming through from the team as they happen.

In my haste to get the new bits, I first went through the nuget package manager and tried updating the ASP.NET MVC package from beta 5 to beta 6 from there. This appears to work, but running my web app resulted in an immediate exception. In my case it was a System.TypeLoadException as follows:

`System.TypeLoadException: Could not load type 'Microsoft.AspNet.Http.Features.IRequestIdentifierFeature' from assembly 'Microsoft.AspNet.Http.Features, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null'. at Microsoft.AspNet.Loader.IIS.RuntimeHttpApplication.ProcessRequestAsync(IHttpContext context)at Microsoft.AspNet.Loader.IIS.HttpApplicationBase.d__5.MoveNext()`

As you'd expect during this intensive development period, pretty much all of the components and dependencies need to move up at the same time, including the .Net Execution Environment (dnx). Luckily, Microsoft have made available a couple of packages: The first will install the beta 6 of the dnx and another will update the Visual Studio 2015 Web Tools component so that new ASP.NET preview Web Project will use the new beta 6 bits for MVC by default.

Simply go to this [Download Centre](http://www.microsoft.com/en-us/download/confirmation.aspx?id=48222) page and download the appropraite packages. In my case, this was DotNetVersionManager-x64.msi (use the x86 version if you are on 32 bit PC or VM) and the WebToolsExtensionsVS14.msi.

Ensure all instances of VS 2015 are closed, install the small DotNetVersionManager package first and then the WebToolsExtensions package.

If you then create a new ASP.NET 5 Web Application from the Preview Templates section, you should find that all the packages are now post-fixed with -beta6, and the Solution DNX SDK version in the Project Properties pane should also be set to 1.0.0-beta6.

As I had an existing beta 5 project, there were a couple more steps to go through:

1. Double-click the project Properties and set the the Solution DNX SDK version from 1.0.0-beta5 to 1.0.0-beta6.
2. Right-click references and choose "Manage NuGet Packages...", Ensure the Package source is set to nuget.org, set the Filter to "Upgrade Available" and check "Include prerelease"
3. Go through and udate each Nuget package with an update available (checking it is set to -beta6 if available). This step is a pretty labourious at the moment!
4. After updating all the NuGet packages I had to then do an explicit package restore by right-clicking "References" and then "Restore Packages"
5. If you have used the Web Application template rather than the empty one, there will be a bit of code fix-up due to breaking changes between Beta 5 and Beta 6 (hey, you were warned :-)!). I used a new Web Application project that was pre-set to use the new Beta 6 bits as a reference and went through and fixed things up. I think it was mainly the Migration files, the Account controller class and the startup class file that needed fixing.

After doing all of the above, my original Beta 5 project now seems to be happily using the Beta 6 bits. Not the smoothest of experiences but such are the perils of being on the absolute bleeding edge!