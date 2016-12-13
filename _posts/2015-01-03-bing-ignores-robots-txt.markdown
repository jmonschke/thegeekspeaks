---
layout: post
title: Bing ignores robots.txt
date: '2015-01-03 06:23:15'
tags:
- microsoft
- google
- bing
- bingbot
---

One of the long-standing conventions on the web is that automated search engine crawlers should follow a set of rules about what pages they should and should not visit and index. For many crawlers or `bots`, all you have to do is properly setup your robots.txt file, and viola, you control what the `bot` will and will not visit. The GoogleBot tends to behave well according to what is in the robots.txt file, but there are others, specifically BingBot that do not.

It seems that as far back as [2012](http://www.webmasterworld.com/msn_microsoft_search/4441555.htm), the BingBot has had webmasters complaining about how it ignores their robots.txt files. 

I have a site that uses Magento's layered navigation to filter the products on each category page, similar to what you would see at [Amazon](http://amazon.com) or [Best Buy](http://bestbuy.com). However, when all those layers are crawled by a crawler, it results in a lot of duplicate information in the indexes of Google and Bing. In addition, it creates unnecessary load on the web servers for pages that the vast majority of visitors never visit.

As a result of Bingbot not following directions, webmasters have a few options, but none are very good. The first is to block all traffic from Bingbot, which would remove you from the search results for Bing, always a bad idea. You could ignore it, spending more on infrastructure to handle the load that Bingbot creates. Or, you could forcibly block BingBot from accessing those URLs that are restricted by robots.txt. It seems that the third option is the best, and is the one to most easily implement in an Apache .htaccess file.