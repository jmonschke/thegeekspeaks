---
date: "2014-10-31T12:34:40Z"
tags:
- mysql
- sql
title: Top 3 Reasons to Avoid Magento's getFirstItem()
---

Magento utilizes a lot of helper functions as well as the Zend Framework and ORM. While this makes things easier to develop, there are areas where this actually makes getting things done more difficult. The very first area that comes to mind is when you are trying to only retrieve a single record from the database. If you were to search Google for the proper way to do this, you would  do the following, assuming `$collection` is your collection object.

```$collection->getFirstItem()```

Here are the top 4 reasons that you should NEVER do this.

1. The very first thing that `getFirstItem()` does is load the entire dataset for the collection. This is not that big of a deal if there are a handful of records that match your criteria, but if you run this against your products or orders or some other model that will have an ever-increasing number of records, you are wasting computing time.

2. It does not take advantage of native SQL functionality for returning a subset of items in a query. Appending `LIMIT 1` to the end of the query and then running that query and returning the single result will be many times faster than loading the entire recordset. For a particular table I have been working with that has over 100,000 records, appending `LIMIT 1` to the end of the query allowed it to complete in 0.03 seconds. However, when trying it the 'Magento Way', the query timed out, providing absolutely no error messages of any kind.

3. Error handling in the `getFirstItems()` function is practically non-existent. Even when you turn on display errors in Magento, if you have a timeout or other issue with the call to `getFirstItems()` absolutely nothing will be displayed or logged. The only way to properly troubleshoot this issue on a remote server that you cannot use xdebug to step through the code line by line is to start commenting code until you figure out what is going on, and you eventually will return to `getFirstItem()` as your culprit.

Here's hoping that Magento 2 will find a way to avoid using this deficient ORM that also has a way of adding 'magic' functions to your system, while also naming other core functions in the same manner the 'magic' functions are named.