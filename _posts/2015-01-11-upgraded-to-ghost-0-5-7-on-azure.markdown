---
layout: post
title: Upgraded to Ghost 0.5.7 on Azure - watch out for npm failing due to older Node
  versions
date: '2015-01-11 23:29:05'
tags:
- ghost-tag
- blogging
---

TL;DR - When upgrading an early installation of Ghost on Azure, make sure the WEBSITE_NODE_DEFAULT_VERSION App Setting is at least 0.10.32 otherwise the npm installation may fail.

I've been meaning to upgrade my slightly ageing 0.4 Ghost deployment to a newer version so as not to get too left behind and make future upgrades less painful!

As an early adopter, I started using Ghost via a manual Git deployment on Azure before it was available in the gallery, so I am hopeful the installation these days should is a lot more straight-forward for most people who want to use this fabulous blogging platform.

I have also become aware of the excellent upgrade utility created by MS employee Felix Rieseberg available at http://www.felixrieseberg.com/the-ghost-updater-for-azure-websites/ and this really makes it a breeze to upgrade to the latest version.

I created a new Azure website and cloned my live site Git repository and ran the update. All worked perfectly so I decided to go for it on live. As is often the case, things didn't quite go as smoothly :-(. Given that the two installations should have been identical, I started checking the logs and looking for differences in the website configurations using the indispensable Kudu utility. One thing that jumped out almost immediately was that my live site was running node version 0.10.5, whereas the newly created test site was using 0.10.32.

After updating the WEBSITE_NODE_DEFAULT_VERSION App Setting value in the Azure Web site configuration screen, and re-running npm install --production from the Kudu console, everything came up perfectly and I have been able to write this quick post which will hopefully help anyone else who get's caught out by this!