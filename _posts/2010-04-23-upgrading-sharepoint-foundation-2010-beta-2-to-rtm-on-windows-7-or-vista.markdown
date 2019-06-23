---
layout: post
title: Upgrading SharePoint Foundation 2010 Beta 2 to RTM on Windows 7 (or Vista)
date: '2010-04-23 18:14:39'
---

As SharePoint Server 2010 and SharePoint Foundation 2010 RTM were released today, I have had a go at upgrading a SharePoint Foundation 2010 Beta 2 installation I had installed on my Windows 7 development environment. This was originally installed in standalone mode due to the restriction with using local accounts (this partition was not domain joined). Standalone mode installs it’s own instance of SQL Server 2008 (called SHAREPOINT) and I was pleasantly surprised that the beta 2 uninstall cleaned itself up pretty well and also removed the SQL instance. I also uninstalled the filter pack 2 beta and a beta of the “Geneva” identity components that I had installed as pre-requisites to the Beta 2 install.

Having uninstalled everything and also made sure there were no SharePoint IIS websites left hanging around or files still in the 14 “root”, I began the process of installing the RTM.

Although I haven’t seen any official guidance, the procedure for installing the RTM on Windows 7 / Vista seems very similar to the Beta to guidance. Once you have downloaded SharePointFoundation.exe, jump to a command line, “cd” to the download directory and run “SharePointFoundation.exe /extract:c:tempspf” (or another directory of your choosing). Once the files have been extracted, open up “c:tempspfFilesSetupconfig.xml” in a text editor and add in the following line:

&lt;Setting Id="AllowWindowsClientInstall" Value="True"/&gt;

Now navigate to “c:tempspfPrerequisiteInstallerFilesFilterPack” and install the “FilterPack.msi” found here.

The final piece is to install the latest identify framework (formerly “Geneva”) from here:

<a title="http://www.microsoft.com/downloads/details.aspx?FamilyID=eb9c345f-e830-40b8-a5fe-ae7a864c4d76&amp;displaylang=en" href="http://www.microsoft.com/downloads/details.aspx?FamilyID=eb9c345f-e830-40b8-a5fe-ae7a864c4d76&amp;displaylang=en">http://www.microsoft.com/downloads/details.aspx?FamilyID=eb9c345f-e830-40b8-a5fe-ae7a864c4d76&amp;displaylang=en</a>

(Obviously you will need the x64 version, and use the 6.1 version for Windows 7 or the 6.0 version for Vista.)

Once you have completed the above 3 steps just run “setup.exe” from “c:tempspf” and follow the install wizard as usual. As mentioned, if you are not running in a domain environment, or you want to use local accounts, you will need to install in standalone mode, unless you use one of the documented workarounds which can be found.