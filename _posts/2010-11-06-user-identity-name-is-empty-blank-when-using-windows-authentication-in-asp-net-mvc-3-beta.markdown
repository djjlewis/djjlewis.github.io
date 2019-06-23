---
layout: post
title: User.Identity.Name is empty / blank when using Windows authentication in ASP.NET
  MVC 3 Beta
date: '2010-11-06 09:34:01'
---

<p>If (like me) you have been tearing your hair out wondering why the User.Identity.Name property always returns an empty / blank string when using &lt;authentication type=”Windows”&gt; in the new <a href="http://www.asp.net/mvc/mvc3">ASP.NET MVC 3 Beta</a> then the answer is surprisingly simple:</p>  <p>As detailed in the <a href="http://www.asp.net/learn/whitepapers/mvc3-release-notes#0.1__Toc274034230">Known Issues</a> section of the <a href="http://www.asp.net/learn/whitepapers/mvc3-release-notes">release notes</a>, just add the following line to the &lt;appSettings&gt; section of the web.config:</p>  <p><code>&lt;</code><code>add</code> <code>key</code><code>=</code><code>&quot;autoFormsAuthentication&quot;</code> <code>value</code><code>=</code><code>&quot;false&quot;</code> <code>/&gt;</code></p>  <p><code><font face="Verdana">Also, make sure you have the &lt;authentication&gt; type set to “Windows” as above, and (optionally) if using the built-in Visual Studio web server (aka “Cassini”) you can also check the “NTLM Authentication” option in the Properties / Web tab.</font></code></p>