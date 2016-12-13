---
layout: post
title: AddThis Can Cause Your Site To Not Load
date: '2014-07-07 01:38:09'
tags:
- responsive-web-design
- javascript
- performance
- web-development
---

Over the last few days, I have run across quite a few websites that seem to never finish loading. After waiting for 20 seconds or more, I give up, realizing that whatever content was on the site wasn't worth it anymore for me to stare at a blank white browser until it loaded however much longer. Unfortunately for those websites, they are losing traffic that they will never get back.

There was one consistent aspect of each of these websites, though. Whoever developed the sites took a bit of a shortcut when it came to adding social sharing buttons to the site. Instead of adding only the social media support the site was active on and implementing this support locally on the site, they used a third-party social sharing provider, [AddThis](http://www.addthis.com). AddThis does make an attractive set of sharing icons that seem to work well when they are loaded on the site. 

However, when these sites implemented the code, the part they forgot to handle was the case when AddThis.com was unresponsive, which is what caused the issues I was seeing. When the web browser makes a request for a standard JavaScript file, all browser rendering and activity is stopped until the JavaScript file is returned. AddThis was responding somewhat in that it was not immediately returning an error, which would have allowed the website in question to continue loading, instead it was responding as if it were going to deliver the JavaScript file eventually, but never did.

When using third-party JavaScript to handle some aspect of your site, always make sure to use the `async` attribute on the `<script />` tag where you include the JavaScript. This tag will ensure that the rendering of the page is not potentially blocked by a slow-loading resource, and will help visitors get access to your site more quickly in many scenarios.