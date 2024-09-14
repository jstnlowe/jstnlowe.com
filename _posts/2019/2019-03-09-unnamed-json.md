---
layout: post
title: "Retrieving Values from Nested Unnamed JSON Arrays"
date: 2019-03-09 20:33:39 -0400
categories: json sql
---

Came across an interesting case where the JSON was an unnamed array of unnamed arrays and the user needed to retrieve a value from within one of those inner arrays.

Here’s the JSON (which we’ll store in the variable `@json`):

{% highlight sql %}

    DECLARE @json​ nvarchar(MAX) =
    [
      [
        {"name": "Supplier","text": "Northstar"},
        {"name": "Product","text": "NS40"},
        {"name": "Material","text": "Steel"}
      ],
      [
        {"name": "Supplier","text": "Qualiton"},
        {"name": "Product","text": "VB-2-AC"},
        {"name": "Material","text": "Aluminum"}
      ]
    ]
{% endhighlight %}

Let’s say we want to grab “Northstar” using [`JSON_VALUE()`](https://docs.microsoft.com/en-us/sql/t-sql/functions/json-value-transact-sql). Unfortunately, we can’t just use that because it can’t deal with the path required, so the first thing to do is to use [`JSON_QUERY()`](https://docs.microsoft.com/en-us/sql/t-sql/functions/json-query-transact-sql) to retrieve the inner array we’re interested in:

{% highlight sql %}
SELECT JSON_QUERY(@json,'$[0]')
{% endhighlight %}

Which returns:
{% highlight sql %}
    [
      {"name": "Supplier","text": "Northstar"},
      {"name": "Product","text": "NS40"},
      {"name": "Material","text": "Steel"}
    ]
{% endhighlight %}

With the above, we can use `JSON_VALUE()` to grab the value we’re interested in:

{% highlight sql %}
SELECT JSON_VALUE( JSON_QUERY(@json,'$[0]'),'$[0].text')
{% endhighlight %}

Which returns: “Northstar”.