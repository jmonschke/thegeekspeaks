---
layout: post
title: Avoid Custom mod_rewrite Rules with Varnish
date: '2015-01-06 02:45:59'
tags:
- varnish
- tips
---

When you are working on a website project running PHP on Apache, and you need to redirect a single device type to a different URL than the rest of your visitors, I'm sure the first thought that many of you would have is to utilize Apache's mod_rewrite. It is a highly flexible URL rewriting engine that would allow you to rewrite with almost any combination of requirements to a just as complex set of URLs depending on the situation.

However, if you utilize a caching solution like [Varnish](http://www.varnish-cache.org), then this may not be a desirable solution. Lets say that that one device visits the url http://www.example.com/something/special and it causes a cache-miss. As a result, Varnish will pass the request on to the Apache web server which detects that you are using the special device, and it rewrites the request to deliver the appropriate special page for the special device. When the Apache web server returns its payload, Varnish takes that as the cacheable value for that specific URL. A few seconds later, a seperate, non-special device visits the page, and instead of getting the non-special payload, it gets the cached version of the special page. The exact opposite scenario could happen just as easily.

This occurs because Varnish's main goal is to reduce the amount of traffic that makes it to your back-end web server. As a result, your Apache mod_rewrite rules are bypassed many times, rendering them useless when you could have multiple different returned results for the same URL requested.

One of the easiest and simplest ways around this is to move your rewriting of the device or browser specific rewrites into your Varnish configuration files. These support the same regular-expression powered custom rewriting abilities that you have with mod_rewrite, but without the caching layer messing things up.

Always make sure to do your rewriting as close to the client's browser as possible. It makes things simpler, and can dramatically improve performance.