---
date: "2014-05-06T01:59:59Z"
tags:
- magento
- performance
title: Unintended Consequences with Magento Observers on Sales Orders
---

Anyone that uses Magento to place orders will be hard-pressed to consider this process a speedy one. While it takes a while to process the order under the best of circumstances, there are a few things that you can do that actually make it worse. 

One of those things that can make it worse is creating an observer that runs in the middle of the saving of the order processes that is always slow-running, or continues to get slower over time as the data that the Magento site grows.  While the observer may run well at first, over time as the data grows, some random symptoms may show up, including database deadlocks and even some missing sales orders. 

Always move any intensive processing tasks outside of the sales order saving process and into a separate process that does not directly interact with the saving of sales orders so that no data is lost.