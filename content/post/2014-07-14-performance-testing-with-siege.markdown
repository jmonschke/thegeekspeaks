---
date: "2014-07-14T01:35:17Z"
title: Performance Testing with Siege
---

One of the most important things to consider when evaluating a website is how well the site performs under load. For many eCommerce websites, there is a higher volume of traffic to the website on Cyber Monday, which is the Monday after Thanksgiving. One of the sites I work with typically sees traffic to its site quadruple on this one day of the year compared to the average traffic. However, when you anticipate something on your site making it to the front page of [Digg](http://www.digg.com) or [Slashdot](http://www.slashdot.org), your site can easily see a jump of an order of magnitude (10X) or more.

So, how do you know how much traffic your web servers that power your site can handle? Well, you could guess based upon past history of peak traffic for your site, but that is extremely unreliable. Instead, you should test the performance of your website's infrastructure and use that as a basis for the current capacity of your site.

One of the best free tools out there to judge the performance of your site is siege. It can be used to simulate many simultaneous users reqesting information from your website at the same time. Its output shows you how well your site was able to respond, what percentage of the time it responded, and the average response time as well as the fastest and slowest responses. In all, it is a pretty informative look at the performance of your web server's ability to generate the content for your site.

The simplest way to run siege is: `siege -g http://www.someurl.com`. This will get the header information returned for the url you are testing against. If you want to run a test against this same URL with 20 concurrent users with no wait in between requests for one minute, you would use something like: `siege -b -c 20 -t 1M http://www.someurl.com`.

If you are interested in finding out more about how to utilize siege and its many options, you can checkout the homepage for [siege](http://www.joedog.org/siege-home/).