---
layout: post
title: Avoid 'Persistent storage maximum size reached' in Firefox
date: '2015-03-03 04:37:37'
tags:
- magento
- javascript
- firefox
- web-development
---

One of the nice tools out there for tracking down issues that your website's visitors are having is TrackJS. We started noticing the other day that we were getting overwhelmed by errors with the text `Persistent storage maximum size reached` for our Magento site. When we looked further into the issue, it quickly became obvious that all of the errors originated from a single user that was running Firefox.

It quickly became obvious that there was a single user that had exhausted their localStorage resources on their browser, but why was it only one user? Well, as it turns out, there is one browser that allows the user to set the amount of space that localStorage can use, and that one browser is Firefox. 

Upon closer inspection, there were several [articles](http://crocodillon.com/blog/always-catch-localstorage-security-and-quota-exceeded-errors) that point out the fact that Firefox implements the exceptions around localStorage differently than other browsers. In fact, the exception code that all browsers other than Firefox throw when they are out of localStorage space is `22`. However, Firefox throws code `1014` instead.

Unfortunately, one of the tools that we use on the site is [history.js](https://github.com/browserstate/history.js/), which makes it easier to update the URL field in the browser due to ajax requests. However, in its native.history.js file, it only checks for error code `22`, causing the uncaught exception in Firefox to bubble to the top where TrackJS finds it and reports it. Simply fix the exception handling in native.history.js and it keeps the exceptions from filling the TrackJS logs.