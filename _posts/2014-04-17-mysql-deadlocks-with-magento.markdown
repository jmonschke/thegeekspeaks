---
layout: post
title: MySQL Deadlocks with Magento
date: '2014-04-17 04:32:47'
tags:
- magento
- mysql
---

One of the things that Magento, and specifically the Zend Framework provide developers is the ability to not have to think about database details as it should just handle all that for you. When it becomes obvious that there is a problem somehow with the production database getting some sort of SQL errors, its time for the developers to start caring about the implementation and architecture details of the database. 
##Symptoms
One of the indicators of upcoming troubles is that your admin users start to get error messages saying that there are deadlocks in the transactions. At first, these errors are extremely sporadic and hard to track down. Over time and increased traffic loads, they will become more frequent to the point that it requires attention.

Fortunately, there is a relatively new Magento extension that enables you to replay the deadlock transactions until they run successfully so that you can get your site back to running properly. While this is not a permanent fix for your issues, as it will slow the site while doing certain actions, it does make the errors stop so that you can fix the root issue. This extension is the [Philwinkle_DeadlockRetry](https://github.com/philwinkle/Philwinkle_DeadlockRetry). I have taken a look at the code and it looks fairly safe, but have not used it in any of my sites, so be careful about deploying it to a busy production site.