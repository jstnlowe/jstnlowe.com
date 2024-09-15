---
layout: post
title: "Single Transaction Processing in SSRS"
date: 2019-01-09 19:02:25 -0400
categories: ssrs
published: true
---

When creating or editing a data source for an SSRS report, there's an option for "Use single transaction when processing the queries". By default, it is not enabled, and SSRS will execute the datasets in parallel, opening one connection to the data source for each.

![Image](/images/2019-01-09.png)

When enabled, SSRS opens a single connection, executes the datasets/queries that use the data source, and closes the connection. The queries are executed in order of appearance in the RDL file (same as in the design view), from top to bottom. This can be useful in certain situations:

- The report datasets or queries contain things like UPDATE statements that make changes to the data being returned.
- You want to reduce the amount of network traffic being generated.
- The report contains a large number of queries that when executed in parallel have an adverse effect on performance.
- There are licensing restrictions that limit the number of concurrent connections to the database

That setting is per data source. Datasets/queries using different datasources will still run in parallel. There are some workarounds for this - for example, using a single datasource and three-part names in the datasets will work if all of the databases you’re hitting are on the same SQL Server instance.