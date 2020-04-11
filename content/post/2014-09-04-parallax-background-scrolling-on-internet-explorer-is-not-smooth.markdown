---
date: "2014-09-04T00:48:05Z"
tags:
- internet-explorer
- jquery
- javascript
- microsoft
- web-development
title: Parallax Background Scrolling on Internet Explorer is Not Smooth
---

One of the pleasures of working on a website that is using some of the latest technologies is that you often run into strange compatability issues that only affect one browser or another, and many of the forums have little to no information about how to properly address the issues. Parallax scrolling is a technique that has been around for a while now, highlighted by Apple's own iPhone 5s card-esque scrolling on their homepage, among others. While the site I am working on does not have as elaborate a parallax implementation, it does not work instantly across browsers by default either.

When the website went into UAT and was thoroughly tested in all browsers, it was discovered that when in Internet Explorer, any time you scroll and the parallax background is visible, the background image jumps up and down. After a bit of searching, it appears that this is caused by Internet Explorer's smooth scrolling feature, and turning it off on my local system resolved the issue for me. Unfortunately, I can't just tell all prospective visitors to my site to turn off smooth scrolling for Internet Explorer, so I had to find a solution that replicated the effects of turning off smooth scrolling.

It turns out that the ideal way to take care of this is to completely hijack the scrolling functionality of pages implementing parallax backgrounds in Internet Explorer, replacing it with some JavaScript or jQuery controlled animations. Effectively, you should first check to make sure that `Trident` appears in the `userAgent`, and if it does, run `event.preventDefault()` on the scroll event on the page, and then replicate the scrolling with the jQuery scroll animation. A sample is shown below:

```
jQuery(document).ready(function () {
    var $html = $("body, html, document");
    if (window.navigator.userAgent.indexOf("Trident") >= 0) {
        $('body').mousewheel(function (event, delta) {
            // disable native scroll
            if (event.preventDefault) {
                event.preventDefault();
            } else { // IE fix
                event.returnValue = false;
            };
            $html.stop().animate({
                scrollTop: $html.scrollTop() + (-delta * 500)
            }, 'slow');
        });
    }
});
````