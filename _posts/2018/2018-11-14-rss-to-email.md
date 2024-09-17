---
layout: single
title: "Sending RSS/Atom Feed Items to Your Email"
date: 2018-11-14 01:56:30 -0400
categories: work
published: true
---

[With the death of Google Reader over five years ago](https://en.wikipedia.org/wiki/Google_Reader#Discontinuation), I hadn't really come across a good alternative (mostly because I hate having to deal with yet another application or site) until I started using [IFTTT](https://ifttt.com/) for some automation tasks. Turns out, you can really quickly create an IFTTT feed-checker that sends new items to you via email. Then, just create a filter for those emails to stick them in their own folder or add a label to them.

To create this type of IFTTT applet, start with the RSS Feed Service, then either “New Feed Item” or “New Feed Item Matches”. Give it the feed URL (and any other specifics if you’re going with the matching item version) and hit “Create Trigger”. Now, we have to tell IFTTT what to do when that thing triggers. Here, you can either use the standard IFTTT Email service or the Gmail service that uses your Gmail account to send the emails from your own account to yourself. That does require granting IFTTT permissions through linking your Google Account, however. Either way, the final step is configuring email filters or automatic labels.

In the end, it only takes a few minutes to set up and you’ll start getting feed items in your inbox (or wherever your filter sends them to). No external app to site to check - just your email.