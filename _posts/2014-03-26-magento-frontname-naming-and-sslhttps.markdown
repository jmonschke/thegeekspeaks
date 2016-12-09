---
layout: post
title: Magento FrontName Naming and SSL/HTTPS
date: '2014-03-26 03:03:25'
tags:
- cache
- magento
- varnish
---

One of the things that has always been an issue for sites that are based on Magento is that they are slow. Well, to be fair, sites using Magento Enterprise Edition that take advantage of the built-in full-page caching functionality seem to have decent page load times. One way to take care of this slow load time issue is to utilize a third-party full-page caching solution such as what [Varnish](https://www.varnish-cache.org/) provides. 
##Varnish
Varnish is a separate caching server that you setup to intercept all of the traffic to your site. It will then forward requests to your web servers, caching any duplicate requests, thus speeding up your site. However, the default configuration of Magento is to make extensive use of cookies to track user activity on the site. Unfortunately for sites that use Varnish, this means that nothing ever gets cached as each request is different. In order to address this drawback, a Magento Module that interfaces with Varnish needs to be installed and configured.
###Turpentine
One such plugin is [Turpentine](https://github.com/nexcess/magento-turpentine) from [Nexcess](http://nexcess.net). It allows you to configure your Varnish settings directly from the admin portion of your Magento site. System messages and other alerts are displayed on the site utilizing a bit of JavaScript injected into the page where the HTML block would typically go, and the JavaScript makes an AJAX request to the server with a unique URL that loads the appropriate non-cached message. This works well for standard Magento blocks and any other blocks you want to show directly within the page. However, if you have data that you want to periodically want to refresh without refreshing the entire page, another approach must be undertaken.
###Custom AJAX Requests
Making a custom AJAX request in Magento is fairly straightforward process. The first thing you would need to do is create a custom Magento module with its own frontend routing. After that, you would need to setup the JavaScript to perform the actual AJAX request. 
If your site is running without SSL turned on for any secure pages, then this next issue will not be one that you run across. If, hoever you do have SSL turned on and configured in Magento, and your custom Magento module also has a backend/adminhtml interface, then there is a chance that you will have issues. When naming your frontend and adminhtml routes, you should be aware that they should not use the same route name, lest Magento get confused about whether the route should redirect to an SSL-enabled page or not. If, on your non-SSL page, you request your AJAX data that has the same route name as the adminhtml for your module, it will be redirected to the SSL version of the block, causing a nasty issue with Cross Site Requests via JavaScript. 
To properly ensure that this is not a problem, you should simply make sure that your adminhtml and frontend route names are different by a single character, and all should work as expected.
