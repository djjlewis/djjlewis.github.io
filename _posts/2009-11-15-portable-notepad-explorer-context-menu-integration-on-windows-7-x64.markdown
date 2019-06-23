---
layout: post
title: Portable Notepad++ explorer context menu integration on Windows 7 x64
date: '2009-11-15 12:53:11'
---

Having just replaced my locally installed Notepad++ with the portable version (see previous post), I wanted to get the explorer context menu working again, so I downloaded the x64 specific version and extracted it into the portable app folder (usually PortableAppsNotepad++PortableAppNotepad++). When I double-clicked reg.bat I was expecting to see the little options dialog appear but instead nothing happened (no error message or anything). After a little trouble-shooting I finally realised that you need to explicitly launch a command prompt session as administrator for this to work.