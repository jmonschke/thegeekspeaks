---
layout: post
title: Unexpected Results with SQL Server and Python pyodbc
date: '2014-04-10 00:40:35'
tags:
- microsoft
- sql-server
- python
---

Using the Microsoft SQL Server Management Studio (SSMS) with SQL Server hides many of the API complications that can sometimes arise when working with SQL Server. One specific example would be when using Python on Windows with the pyodbc driver. If you have an update statement that performs a simple update to a status column and a datetime column, you can have some unexpected results.

Lets say that the table you are running the update against has a before update trigger and an after update trigger configured on it. Both triggers effectively do the same thing, as they log the current affected row to a second, logging table, peforming separate insert statements to do so. When running this update statement in SSMS, it seems to behave as you would expect, with a single result set returned, but listing three sets of (1 row updated) for every row that was updated. When using Python's pyodbc driver to run this exact same SQL update statement, it shows that only 1 row was updated when there should have been many updated.

It turns out that Python's pyodbc driver's `execute` statement has an interesting way of functioning in that it only expects a single result set coming back from SQL Server. Interestingly enough, it also treats each line of the (1 row updated) as a single result set, so it thinks that there were 3 result sets for ever row updated. Unfortunately, when Python's pyodbc code sees the multiple result sets, if you are in a transaction, it seems to rollback the transaction, erasing any trace that the problem existed, and then move on to the next piece of code.

Stored Procedures allow us to move the SQL query definition out of the Python codebase and into SQL Server, allowing us to hide the fact that there are multiple result sets generated for this simple update query. While this can make it more challenging to audit the changes to the SQL query that is run if you do not have a proper SQL Source Control management plan, it has other benefits as well. The biggest benefit is that you are able to run the query described above without issues, but almost as importantly is that Stored Procedures tend to perform better than an ad hoc SQL query as SQL Server is able to cache the execution plan for the Stored Procedure and reuse it, as opposed to recreating it for every run of the ad hoc query.