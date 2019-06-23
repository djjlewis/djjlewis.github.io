---
layout: post
title: Assembly Binding
date: '2009-07-30 11:03:43'
tags:
- net-development
---

Today I had an issue with an old app that referenced an assembly (A) but also contained a reference to assembly (B) that also contained a reference to assembly (A)!.

The problem was that assembly (B) reference an earlier version of assembly (A) than the app itself, and I was able to recompile this against the new version.

Luckily a quick assembly binding  addition to the app.config saved the day.

All you need to do is add the following lines to your app.config (or web.config for asp.net):

&lt;runtime&gt;
&lt;assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1"&gt;
&lt;dependentAssembly&gt;
&lt;assemblyIdentity name="[name]" publicKeyToken="[token]" culture="neutral" /&gt;
&lt;bindingRedirect oldVersion="1.0.0.0" newVersion="1.0.1.0" /&gt;
&lt;/dependentAssembly&gt;
&lt;/assemblyBinding&gt;
&lt;/runtime&gt;