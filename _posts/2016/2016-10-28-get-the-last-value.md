---
layout: post
title: "Get the Last Value from a Spreadsheet Column"
date: 2016-09-13 17:27:09 -0400
categories: excel google-sheets
---

The following will get the value of the last populated cell in a column regardless of the data types in the column or if there are empty cells among the populated cells.

Microsoft Excel
{% highlight plaintext %}
=LOOKUP(2,1/(NOT(ISBLANK(A:A))),A:A)
{% endhighlight %}

Google Sheets
{% highlight plaintext %}
=INDEX(FILTER(A:A,NOT(ISBLANK(A:A))),ROWS(FILTER(A:A,NOT(ISBLANK(A:A))))
{% endhighlight %}