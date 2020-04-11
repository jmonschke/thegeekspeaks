---
date: "2014-04-14T21:43:02Z"
tags:
- magento
- varnish
- performance
title: Varnish and Magento Performance Mystery
---

One of the things that you think you will solve when you implement a Varnish caching server in front of a Magento website is performance problems. However, this is not necessarily the case.

When I set Varnish up to cache content in front of my Magento website, I get what seems to be much improved performance. If I run a few tests in the developer tools of Chrome, it seems that the waterfall chart makes sense and the data is loaded appropriately and in a timely manner with the main HTML being downloaded in about 300ms. 

This all seems well and good until I go try to validate my results with a third party testing platform, namely webpagetest.org. When you run the test with Chrome and with native bandwidth, you will see that the page loads much more slowly than it does on your local system, and in fact, it shows that the HTML download for the site no longer taks 300ms, but instead takes 2-3 seconds to download. 

The solution to this issue? Well, at this point, I just wish I had one. From what we are seeing using various analytics tools, the site is loading faster, but it does not seem to show the same site load times that webpagetest.org does.