---
layout: post
title: "Converting Perfmon BLG with Relog"
date: 2019-04-16 13:56:01 -0400
categories: perfmon relog
---

Relog is a great, probably underutilized utility that ships with Windows (`\Windows\System32\`). It lets you take just about any system performance log file and convert it to a number of formats (including dumping them into SQL). It also supports resampling, however the resampling (with `-t`) does not involve any sort of statistical operation; it just takes every nth sample. For example, a 1-min interval log with `-t 60` specified would take every 60th sample in the log, effectively giving you a 1-hour interval.

Converting perfmon blg files to csv:

`\nrelog logfile.blg -f csv -o logfile.csv`

Importing to a SQL store requires first that you create a SQL Server ODBC DSN:

`\nrelog logfile.blg -f sql -o SQL:!`

Taking a logfile with 1 minute sample frequency and resample to a 1 hour frequency csv:

`\nrelog logfile.blg -f csv -o logfile.csv -t 60`