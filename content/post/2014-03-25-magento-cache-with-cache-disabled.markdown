---
date: "2014-03-25T02:02:20Z"
tags:
- cache
- magento
title: Magento Cache with Cache Disabled
---

One of the things that I find quite annoying with a web platform is when you configure it to do one thing, and it does something different. [Magento](http://magento.com) is an eCommerce software platform that many of the leading eCommerce websites use for their web stores.
##Magento
Magento comes in two different flavors, a paid enterprise edition as well as a open-source community edition. The enterprise edition allows you to utilize the built-in full-page caching mechanism, while the community edition does not include a full-page caching solution.

###Caching in Magento
Standard caching in Magento allows you to cache configurations, layouts, blocks, translations, collections, EAV Types, and web services data. One would think that when you disable each of these types of caching, then there would be nothing cached any longer. Unfortunately, when all caching is disabled in the admin UI, there is some caching that still takes place. In fact, the  database schema for Magento's ORM is cached no matter how your site's caching is configured.

In the process of developing the schema for a new module, it sometimes becomes useful to modify the SQL setup files for the module without creating a new upgrade script. Before expecting that the changes will take place immediately, make sure to flush the Magento cache, even if all of the caching is disabled.

This is one of those things that you only need to experience once to remember it for the future to keep from having to repeat the maddening search for what is causing the changes to not take effect. Hopefully this will help someone to figure out why their table's datatype changes are not taking effect or some other database change is mysteriously not working.