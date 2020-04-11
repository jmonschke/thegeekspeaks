---
date: "2014-06-23T01:47:49Z"
tags:
- jquery
- responsive-web-design
title: Always URL Encode your Cookies
---

One of the things that you tend to forget about when dealing with websites that typically only cater to English-speaking visitors is how to properly deal with Unicode throughout the site. It turns out that some browsers handle Unicode support in different sections of the browser differently.

For instance, it turns out that when you want to store Unicode data as the value in a cookie, your success may vary across browsers. When I tested this with the Euro symbol, €, it worked without a hitch in Chrome, Safari, and Internet Explorer. However, in Firefox, it was stored as an empty string. In order to correct the issue, you can use `encodeURI()` on the Unicode character to get the ASCII version of the Unicode character, and then store that in the cookie. Fortunately, this seems to work without issue across all of the major browsers.