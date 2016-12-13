---
layout: post
title: Avoid SQL Deadlocks -- Break Up Large Updates
date: '2014-05-08 02:19:46'
tags:
- sql-server
- mysql
- sql
---

Deadlocks in SQL occur when one query locks certain rows, frequently for updates, and a second query tries to update those same rows. The second query will then create an error as those rows are unable to be updated since they are in the middle of an update from another query. One of the surefire ways to create a slow running update query like the first query above is to hava a single update statement that will update a large number of rows at once.

I have seen a table that has over 1.5 million rows that frequently had deadlocks with update statements. The query that it seems was the cause of these deadlocks was an update statment that updated over 250,000 rows all at once, taking 30 seconds or more to execute and running at least once an hour. While the schema of this table is in need of a major update, it must work in its current state without opening these large windows for deadlocks to occur.

The update query, unfortunately, must run regularly to update some constantly changing data. This query does a few joins to other tables, and as a result, the version of MySQL that it is hosted on does not support limiting the update statement when it does joins. As a result, in order to break the update statement into chunks as small as 1000 rows at a time, you must first stage the data in a temporary storage location. Once the updated data is consolidated into the staging table, you can then perform the insert into the large table at a small chunk of rows at a time. While preparing the staging table still takes about 30 seconds, this does not expose the server to deadlocks. The actual inserts from the staging table, if performed all at once takes only about 4 seconds. If we break it into chunks of 1000 rows at a time, the overall time for the update is still around 4 seconds, but the individual updates only take a couple hundredths of a second to complete, making it extremely unlikely that a deadlock will occur.

In the end, I was able to perform the update of over 250,000 rows in about 4 seconds without much chance of instigating a deadlock that previously was almost guaranteed to occur.