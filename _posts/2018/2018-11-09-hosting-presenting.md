---
layout: post
title: "Hosting & Presenting"
date: 2018-11-09 21:10:56 -0400
categories: work
---

I've sat through a lot of web meetings. A lot of software demos, a lot of Powerpoints, a lot of webinars. I would say that the vast majority of the presenters (easily 9 out of 10) show little awareness for the things they're inadvertently revealing to their attendees. It's a disregard for the disclosure of information that, in some cases, could be considered straight-up negligence. And it has nothing to do with how terrible their Powerpoint slides are.

They'll use the default full-screen or full-monitor sharing mode most of the time because they don't know about or don't understand the various features of their meeting software that are specifically designed to limit what is shown (e.g. the ability to share a specific application instead of the entire screen). They'll present from whatever computer and whatever environment they do their daily work in. They'll switch application windows during a demo and maybe reveal their desktop as they do so. Maybe switching windows leaves their email client or an open document visible for just a moment as they find the application window they want to show.

Their browser favorites might be visible. The browser itself might auto-fill fields during a demo or reveal details of their browsing history. That's all information that they just inadvertently shared with all of their attendees. And that matters, because if something's visible during your screenshare, even for a second, even if it's only visible as part of some flashy OS transition effect, you should assume that an attendee now has a record of it and that the contents are now known to them. And I say all of this because I am that attendee. If you inadvertently reveal something, I probably grabbed a screenshot of it if the session isn't already being recorded (shout-out to [Greenshot](http://getgreenshot.org/) and [ShareX](https://getsharex.com/)).

The information I've derived from screenshots ranges from the innocent and humorous - like the browser revealing that they frequently visit Pornhub or search history revealing that they didn't know "how grass makes more grass".

![Image](/images/2018-11-09-01.jpg)

To some very inappropriate comments about a colleague in an email conversation.

![Image](/images/2018-11-09-02.jpg)

To little individual things that, when taken cumulatively, allow someone to derive sensitive information - like the names of open Word documents at one point in the presentation followed by the icons on the desktop indicating that some bad HR stuff was about to go down later that week. To straight-up DEFCON-1-call-your-IT-director-immediately.

_Like an open text file with VPN credentials. Followed by the IP addresses, RDP ports, and admin logins for every single one of a major organization’s servers._

![Image](/images/2018-11-09-03.jpg)

Yes, I notified the appropriate people immediately. During the presentation, in fact. _But there were sixteen other attendees in that meeting._ That’s a whole lot of room for “what if”, because if I’m doing it then I think it’s prudent to assume that everyone does it. And not everyone is going to treat the situation responsibly. What it comes down to is that if you’re a presenter or a host, you must be acutely aware of what you’re sharing.

# Know Your Software
Figure out how the screen-sharing settings work and understand what they do. Become adept at switching between sharing options and knowing what settings are appropriate for a given situation. Set up and join your own web meeting so you can see exactly what attendees would see with the various functions. Better yet, get some colleagues in on this so that they learn something here as well.

# Present from a Clean Environment
Use a separate user account, a virtual machine, or even a different physical computer to present from. One that is only used for that purpose and nothing else. An environment that contains nothing but the software and content you need for that specific meeting or presentation. Depending on your situation and your skill level, this might not be possible. In which case…

# Prep Your Environment in Advance
If you don’t have a separate environment for presentations and are going to be using the same one you use daily for work, you need to reduce the potential information that could be leaked. Hide your desktop icons, clear your browser history (or use a different browser entirely), clear recent documents and recent programs lists, close absolutely everything that isn’t relevant to that meeting. If you’re demoing software, be cognizant of the things you’re going to be doing that could reveal information - like opening or importing a file into the program that first presents you with a file browser.