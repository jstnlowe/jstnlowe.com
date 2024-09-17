---
layout: single
title: "Create Individual Archives of Subfolders"
date: 2018-10-03 20:16:25 -0400
categories: powershell
published: true
---

This Powershell command will use [7-zip](https://www.7-zip.org/) to create individual zip archives of all folders within the current directory. Not sure why this is not a GUI option with 7-zip or an option from the context menu. We need to use a conditional statement to prevent it from adding the archives you just created to themselves and just looping forever (well, until you run out of space on that drive).

{% highlight powershell %}
dir | ForEach-Object { & "7za.exe" a $_.BaseName $_.Name }
{% endhighlight %}