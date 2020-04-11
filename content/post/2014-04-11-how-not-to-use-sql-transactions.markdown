---
date: "2014-04-11T02:20:17Z"
tags:
- microsoft
- sql-server
title: How Not to Use SQL Transactions
---

SQL Transactions allow you to isolate atomic operations so that you can ensure that a third party does not update the data affected during the atomic operation protected by the transaction. An example of an operation that you would want to protect with a SQL Transaction would be transferring funds from one bank account to another. The first step of this operation would be to subtract the funds from bank account A. Once complete, we would then add the same amount of funds to bank account B. Assuming nothing fails, everything works as expected. However, if there is other database activity at the same time or an error occurs in one of the queries, without a transaction you could have the funds removed from bank account A or added to bank account B, but not both, causing a major balancing issue with your bank accounts.

If you were to wrap this operation in a transaction, and one or both of the queries failed, the changes that were successful were undone, and the bank accounts stay in balance.

It always surprises me when I find incorrect or ineffective use of SQL Transactions in production software applications. If, in the example above, you put a transaction around removing funds from bank account A and another one around adding funds to bank account B, and there is an error in either one of the queries, the other will go through without issue, causing the problem described above. Amazingly, this is the way an application was implemented causing issues sporadically.