---
layout: post
title: Don't Be a Dunce, Save Your Orders
date: '2015-03-05 03:55:45'
tags:
- magento
- web-development
- php
---

There are some gotchas that you think that you will always see coming. One such gotcha is the need to save an object to the datastore to persist any changes you may have made to that object.

While it seems like a reasonable concept at the base level, there are times that the need to save an object completely escapes your mind. It seems that for many non-developers, this occurs when they have been working a long time on a file, typically a Microsoft Word document, shortly before their computer blue screens, losing all of their work.

In this case, it luckily had nothing to do with Microsoft Word or a blue screen. Instead, I was trying to programmatically add a comment to an order in Magento. I kept triggering the code that should add the comment over and over, unable to find the comment on the order, and noticing that there is nothing logged to any of the Magento log files. Finally, after spinning my wheels for a bit, and checking with a co-worker, it became obvious that the issue was that I was not saving the order, ensuring the comment that I just successfully added to the order was lost forever.

In case you wanted to know how to properly add a comment to an order without notifiying the customer or allowing the customer to see the comment on the frontend, here it is:

```
$order->addStatusHistoryComment('Order Comment Here', false)
    ->setIsVisibleOnFront(false)
    ->setIsCustomerNotified(false);
```
