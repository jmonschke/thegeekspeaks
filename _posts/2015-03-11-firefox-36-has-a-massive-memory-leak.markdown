---
layout: post
title: Firefox 36 Has A Massive Memory Leak
date: '2015-03-11 03:22:51'
tags:
- javascript
- firefox
- web-development
---

While looking through our [TrackJS](http://trackjs.com) logs the other day, I ran across a peculiar error message coming from Firefox 36 on Windows 7. The error message was simply `out of memory`. It seemed that the pesky [local storage](https://thegeekspeaks.net/avoid-persistent-storage-maximum-size-reached-in-firefox/) issue had reappeared mysteriously. However, with a quick check of the codebase, I verified that no one had accidentally reverted those fixes.

With that possible cause ruled out, I turned to a developer's best friend, Google, for solutions. Well, it appears that Firefox 36.0.0 has quite the [memory leak](https://bugzilla.mozilla.org/show_bug.cgi?id=1137251) issue. When looking into the detail of the issue, it became highly probably that this issue was the cause of the errors in our monitoring tools. Apparently, this bug rears its ugly head when you are doing 2D rendering on your page, and the site uses a 2D charting library to present information.

According to Mozilla, Firefox 36.0.1 should resolve this memory leak issue and has been released for public consumption. Upgrade Firefox today!