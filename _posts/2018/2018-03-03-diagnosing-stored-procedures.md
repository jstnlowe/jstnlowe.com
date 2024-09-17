---
layout: single
title: "Diagnosing Slow-Running Stored Procedures"
date: 2018-03-03 13:47:21 -0400
categories: sql
published: true
---

This week, I had a stored procedure taking 2 to 3 seconds to execute from a .NET application, where it previously took under 40ms. A few seconds doesn't seem that long, but the application was looping through a collection of items and calling the procedure around a hundred times. Meaning for the user, the time to complete the workflow had increased from around 4 seconds to over 4 minutes. Nothing had changed with the tables being used and index fragmentation was not an issue, thanks to fairly aggressive maintenance plans.

What was more baffling was the same process looping the same stored procedure used in the same application installed in a test environment took the expected four seconds or so. In SSMS, in both production and test environments, everything was well-behaved. Firing up the profiler, I could see that the sproc was reading around a thousand records when executed from SSMS (regardless of environment), but when the .NET application ran it, it was reading 250,000.

The culprit was the execution plan. Or rather plans. Plural. SSMS was getting one plan and the .NET application was getting another. To figure out why SQL was using two separate plans, you need to get the handles for the plans for the stored procedure:

{% highlight sql %}
SELECT sys.objects.object_id, sys.dm_exec_procedure_stats.plan_handle, [x].query_plan
FROM sys.objects
INNER JOIN sys.dm_exec_procedure_stats ON sys.objects.object_id = sys.dm_exec_procedure_stats.object_id
CROSS APPLY sys.Dm_exec_query_plan(sys.dm_exec_procedure_stats.plan_handle) [x]
WHERE sys.objects.object_id = Object_id('StoredProcName')
{% endhighlight %}

From there, consulting the `SET` options for the plans revealed something interesting: one plan had `ARITHABORT ON`, the other `ARITHABORT OFF`. SSMS, by default, has it set to on. Client applications have it set to off. The result was that SQL was using a horrifically bad execution plan for the .NET application and a reasonable one for SSMS. This is usually tied to issues with the parameter sniffing that SQL uses when compiling a plan. The solution I decided to go with was to queue the sproc for a plan recompile:

`EXEC sp_recompile N'StoredProcName'`

The next time the sproc was executed, SQL generated a new plan for it. The result was a drop from 250k reads and 3 seconds per execution to around a thousand reads and under 40ms. Exactly what it should be.