---
layout: post
title: Magento appending __SID to URLs
date: '2014-04-23 02:39:33'
tags:
- cache
- varnish
---

When trying to fully optimize a Magento website to run as fast as possible, I tend to opt for turning on all of the caching options in Magento, and then put the Varnish caching server in front of the web server with the Turpentine plugin. However, when you do this with some configurations, you start seeing the `__SID` query string parameter added to the end of the site's url. Unfortunately, when the Turpentine plugin sees the `__SID` query string in the URL, it means that this page request will bypass the cache and load it directly from the server, slowing things down.

The particular configuration that causes this issue is when the setting to "Use SID on Frontend" is set to "YES". If you are only running a single web store on your Magento installation, then you can safely change this to "No". However, if you have multiple web stores on this same installation, users will lose the ability to log in to one store and then navigate to the other one without having to log in to the second store. If this is not a problem for you, you can safely set this to no. After changing the configuration, you will want to refresh all your caching mechanisms, and once you do so, the `__SID` query string parameter should no longer be added to your URLs, allowing your site to load much faster overall.