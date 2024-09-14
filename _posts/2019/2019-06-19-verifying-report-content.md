---
layout: post
title: "Verifying Exported SSRS Report Content"
date: 2019-06-19 13:32:20 -0400
categories: vmware troubleshooting
---

When it comes to the generation, export, and/or printing of reports, there are times when it is useful to be able to quickly determine the contemporaneity and integrity of a report. This is useful in situations where you need to determine at a glance if the contents of the report are recent and or if any changes have been made to them.

There are much more powerful and comprehensive ways of ensuring report/data integrity, however the following applies to situations where "casual" inspection of a report is sufficient. What I’ll cover here is the use of a timestamp and the generation and use of a hash value.

# Time Generated

Including a timestamp of report generation is a very common approach and, depending on how often that report is generated or the content is updated, displaying just the date may be sufficient. This can be accomplished through the use of SSRS global parameter ExecutionTime. I almost always include this in the footer of the reports I design, typically in a smaller font so that it does not distract the user from the contents of the report.

# Content Hash
When it comes to validating the contents of the report, the approach that I tend to use is to call SQL's [HASHBYTES()](https://docs.microsoft.com/en-us/sql/t-sql/functions/hashbytes-transact-sql) function, passing it values from the report. While in many cases you may be able to pass the full contents of the report into the function, the input is limited to 8000 bytes so you may end up having to choose a subset of values. An added bonus of using a subset is that, as long as you do not indicate which values were used, it makes attempts to falsify a hash all that more difficult (not that this is a practical concern for most applications).

The output of the function is a value that is (in practice) unique to the input which allows for the verification of the contents of the report: the hash on a previously-generated copy could be used to very quickly determine if the contents of the copy had been modified externally after generation or if the values in the database had been changed since its generation.

As of SQL 2016, the weaker hash algorithms have been deprecated, leaving us with SHA2\_256 and SHA2\_512 both of which have output that is not human-readable and not suitable for displaying on a report. To address this, it's perfectly acceptable to truncate the hash to a more reasonable length for our purposes.

# Implementation

Let’s say that we have a report that displays the contents of a single personnel record. The dataset query looks like this:

{% highlight sql %}
SELECT [Id],[FirstName],[LastName],[Username],[HireDate],[AccessLevel],[Notes]
FROM [Employees] WHERE [Id] = @userid
{% endhighlight %}

Now, let's say that our primary concern is the integrity of the `[AccessLevel]` and `[Notes]`. We'll include the following line in the SELECT statement to generate the hash using SHA256, convert it to varchar, and truncate it to the first sixteen characters:

{% highlight sql %}
LEFT(CONVERT(VARCHAR(64),HASHBYTES('SHA2_256',[AccessLevel]+[Notes]),2),16) AS [ReportHash]
{% endhighlight %}

The output could then be displayed in the footer of the report alongside the generation timestamp and would look something like this:

`3A250D547F4A209A 06/03/2019 19:01:35`