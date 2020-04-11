---
date: "2015-03-23T01:44:34Z"
tags:
- javascript
- chrome
- google
title: Google Chrome Improves JavaScript Speeds Again
---

One of the old rules of optimizing website load times for all browsers was that the browser didn't begin to parse the downloaded JavaScript until each file was downloaded. Starting with Chrome 41, Google has announced that this is no longer the [case](http://blog.chromium.org/2015/03/new-javascript-techniques-for-rapid.html).

In this announcement, Google has said that new versions of Chrome will begin parsing JavaScript as it is downloaded to the browser, even before the particular file's download is complete. However, in order to see this happen more quickly, you must utilize the `async` or `deferred` tags in the `<script>` tag. JavaScript that is loaded without `async` or `deferred` is still a completely blocking action that pauses all rendering while downloading and parsing the JavaScript files. According to Google, this can improve website load time by up to 10%.

In addition, Chrome will now keep a copy of the parsed JavaScript in its cache for future use on additional visits to the same page. While this will improve secondary load times on a page, it sounds like it will not improve page load times when the same script file is loaded across multiple pages on the site. We can only hope that Google is able to add that functionality to Chrome, which should definitely make a significant difference in page load times.