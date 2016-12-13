---
layout: post
title: Magento Version 2, is it just Microsoft Windows Longhorn AKA Vista?
date: '2014-05-02 02:10:03'
tags:
- magento
- rant
- windows-vista
---

Magento version 2 was first introduced in 2010. It is now almost halfway through 2014, and the public has not seen any alpha or beta release of Magento version 2 as of yet. The new version of Magento promised to replace PrototypeJS and Scriptaculus with jQuery as well as reorganize the database schema to remove the slow EAV tables and migrate to a bit of a flatter table structure. However, it seems that the latest updates on the direction for Magento 2 show that the database schema will not be changed much after all. 

[All You Need to Know About Magento Release 2](http://www.cloudways.com/blog/magento-2-development-update/) is the most recent news about anything related to Magento 2, and it is quite sparse in detail from the Magento 2 team and eBay. However, the one big piece of news about the Magento 2 release is that the Magento team is removing the `Mage` class, and completely replacing this root parent class with a new class structure that should make upgrades easier once your site is on Magento release 2. Unfortunately, this also means that upgrading a Magento 1.x site to Magento 2.x will be a large project, as every plugin will have to be rewritten to remove their reliance upon the `Mage` class. More information about what will be required to upgrade from [Magento 1.x to 2.x can be found here.](https://wiki.magento.com/display/MAGE2DOC/Magento+1.x+to+2.x+Backwards-Incompatible+Changes)

Considering the fact that the upgrade process to Magento 2 will require a total rewrite of each Magento installation, it reminds me of one of Microsoft's failed new operating systems, [Microsoft Windows Vista (CodeName Longhorn)](http://www.betaarchive.com/wiki/index.php?title=Windows%3ALonghorn). Magento 2's development timeframe seems to share Longhorn's, and lets hope that the finished project is much better than Microsoft Windows Vista, one of the worst operating systems Microsoft has released. 

One good piece of news out of Magento is that Magento 1.x will be supported for 3 years after Magento 2.x is released. At this point, it seems that it is not out of the realm of possibility that Magento 1.x will still be supported in 2019 or 2020.

You can keep up with all the goings ons and updates to Magento 2 [here](https://github.com/magento/magento2).