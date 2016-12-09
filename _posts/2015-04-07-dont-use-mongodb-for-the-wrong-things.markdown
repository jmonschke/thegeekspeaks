---
layout: post
title: Don't Use MongoDB For The Wrong Things
date: '2015-04-07 01:39:20'
tags:
- javascript
- design-patterns
- web-development
---

The early phases of a greenfield project always seem to conjure up grand ideas of how to use the hottest new technologies to accomplish your goals. Many times, these grandiose plans give way to a more level-headed design discussion where more realistic technologies are adopted. However, there are a few times where the developer with the idea to use the hottest new technology is the one in charge, and ends up getting his way.

Unfortunately, this seems to happen too often in the NoSQL vs RDMS wars. It seems many of the proponents of a NoSQL solution seem to think that you can use your favorite NoSQL datastore, say MongoDB, as a replacement for a relational database. Granted, there are many situations where MongoDB would be an adequate solution for your project and where a relational database would be overkill. However, these scenarios are a lot less common than many seem to think.

>Don't try to innovate with the platform you are building your solution with, innovate with your solution.

When working with a NoSQL solution such as MongoDB, the danger lies in trying to use MongoDB in a project that has an immense amount of *related* data. While it may seem like a CMS would be a perfect situation to utilize MongoDB, in reality, there are quite a few relationships that exist in even the most basic of websites. Many times, pages are grouped into categories, and then further grouped by date and/or author. It may seem trivial to just add this information to the document that is stored for each page, but if you need to update the author's name on all of the posts that they wrote because they had a change in their legal name, it would take some work to update each page's document. If, however, you wanted to show all of the pages that a single author contributed to, you can still do it in MongoDB, but it just adds another level of relationship to data that is supposed to not be relational.

The scenario that you absolutely do not want to use MongoDB is when you are working with financial or other multi-part transactions that must either go all the way through to completion or return an error and save no history of the transaction's effects on the data moving forward. An eCommerce platform would be a perfect example of when you absolutely want transactions to complete for an entire sales order instead of partial completions. A partially complete sales order would cause developers many lost hours trying to figure out which customer tried to order which product and with which payment method that got lost. Relational database systems provide a standardized method for doing this, allowing developers to base their designs on industry best practices.

While there are valid use cases for MongoDB and other NoSQL database stores, they are not the right choice for many projects. Don't try to innovate with the platform you are building your solution with, innovate with your solution.