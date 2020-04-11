---
date: "2014-08-21T01:16:01Z"
tags:
- jquery
- javascript
- rant
- chrome
title: Google Chrome Makes Web Developers Lazy
---

This post may make me sound ancient in the world of web development, but here it comes anyway. 

>Like Microsoft, Google has decided to implement functionality in their dominant browser that is incompatible with the other major competing browsers.

When I first started developing websites professionally, ensuring a website worked for 99% of the site's visitors was easy, relatively, as you only needed to make sure the site worked in Internet Explorer 6. Obviously, there were a ton of random hacks and tricks required to deal with the quirks of this browser, but you were fairly safe knowing you had developed your site to be tailored to the browser of choice for your visitors. However, the dominance of Internet Explorer 6 was bound to come to an end and it ushered in an era of multiple popular browsers including Firefox and Chrome. With no single browser having a massive advantage in terms of users in all areas, web developers had to make sure that thorough testing of their sites was completed in each of the major browsers.

>It works in Chrome, so it's good enough.

Fast forward to 2014, and depending on the website, but we are almost in the same position we were in with a dominant browser we were years ago, but this time that dominant browser is Google's Chrome browser. Granted, the Chrome browser of 2014 brings with it a much more powerful set of developer tools than we could dream of with Internet Explorer 6, but, like Microsoft, Google has decided to implement functionality in their dominant browser that is incompatible with the other major competing browsers. Now that Chrome is so popular, especially among web developers, I will often run across websites that make it obvious they were developed to the point of "it works in Chrome, so it's good enough".

>Many web developers don't know how to properly test their own websites.

One such area that I have seen this occur is with jQuery's event handlers and JavaScript that assumes global variables exist. Here is one such example:

```
$(".link").click(function() {
    event.preventDefault();
});
```

Most experienced JavaScript and jQuery developers would quickly notice that this code will cause an exception when anyone clicks on an element with the `link` class. Unfortunately, in order to know the complete answer, you would have to know the exact quirks and 'features' that have been added to the browser to make things a bit easier for developers. The answer here is that in Google Chrome, the above click handler will function normally without any unintended side effects as Chrome has implemented a global `event` property that keeps this from throwing an exception.

> Web developers should thoroughly test their sites in all the major browsers that their users use, fixing issues before they come to the attention of QA and end users.

If you were to test this code in Firefox, you would get the result that would be expected behavior, which is to get an error saying that `Cannot read property 'preventDefault' of undefined`. Keep in mind that I ran across this beauty in a website that was in its final testing stages before going live. Whenever I see issues like this it reinforces a long held opinion that many web developers don't know how to properly test their own websites. The correct version of the above code is below:

```
$(".link").click(function(event) {
    event.preventDefault();
});
```

The excellent functionality that the Chrome devTools provide web developers and the 'mostly' standards-complaint functionality of the Chrome rendering engine have made it so that many web developers simply develop their website for Chrome, and then wait for QA and the public testers of the site to report any cross-browser issues. Instead, web developers should thoroughly test their sites in all the major browsers that their users use, fixing issues before they come to the attention of QA and end users.