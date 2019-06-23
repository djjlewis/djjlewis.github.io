---
layout: post
title: Error messages connecting to Hyper-V Manager
date: '2010-08-16 12:44:40'
---

At work, I have Lenovo ThinkStation running Windows Server 2008 R2 Core along with the Hyper-V role and a number of VMs (primarily for SharePoint 2010 development). After being on holiday for a couple of weeks I started up Hyper-V manager but was greeted with the one of the standard “Cannot connect to the RPC service on computer ... Make sure your RPC service is running” messages. No problem, I thought, I’ll just RDP to the host direct and check out what was going on. Having then tried to RDP with my standard user account, I was then greeted with the message “An authentication error has occurred. The Local Security Authority Cannot Be Contacted” which I don’t recall ever having seen before! I then tried to RDP using the local administrator account and it went through fine. Something very strange was going on here!

After a couple of minutes trying and retrying my normal user with no luck, it suddenly struck me that either the user account’s password had expired in the 2 weeks I was away, or I had inadvertently locked the account.

As Server Core is not the easiest thing to manage and easily check these things, I ended up running two different NET USER commands in case it was one or the other. Most user and group operations can be performed from the command line using NET USER or NET GROUP. For a list of all available commands just run NET HELP USER (or GROUP).

The first command simply changes a user accounts password in the event it may have expired. It appears you can set this to the previous password anyway, as this is what I did:

NET USER [username] [password]

The second command will reactivate an account in case it has been disabled:

NET USER [username] /ACTIVE:Yes

Having run the above two commands, I was then able to log back in via RDP and use Hyper-V manager again through my standard user account.