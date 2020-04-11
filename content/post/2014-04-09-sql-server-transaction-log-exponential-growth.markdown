---
date: "2014-04-09T01:35:42Z"
tags:
- microsoft
- sql-server
- python
title: SQL Server Transaction Log Exponential Growth
---

There are few things more frustrating than seemingly random issues that crop up in software when configuration changes occur. One such occurrence is when you migrate your databases from Microsoft SQL Server 2012 Standard Edition to Microsoft SQL Server 2012 Enterprise Edition with High Availability and the transaction log suddenly begins to experience exponential growth without ceasing.

It turns out that when using Python and pyodbc on Windows to access SQL Server, there can be some unpredictable results. If you have a long-running SQL query that you are running from Python and pyodbc, when you are running it against a Microsoft SQL Server 2012 Standard Edition database, it will fail and time out silently, making Python think that the query succeeded. On the other hand, if you run the same long-running SQL query from Python and pyodbc in Microsoft SQL Server 2012 Enterprise Edition with High Availability, it will fail and rollback the query, but will fill the transaction log.

To resolve the issue, you can take care of the speed of the long running query and all is fine.