---
date: "2014-10-07T01:44:40Z"
tags:
- javascript
- html
- safari
- apple
title: LocalStorage and Safari Weirdness
---

One of the technologies that has been intriguing to me for a while has been LocalStorage on the web browser. One of my first adventures into using persistent storage other than cookies on a web browser was the short-lived HTML 5 standard of the webSQL database. It turns out that it was simply a SQL Lite database that was accessible via JavaScript in all the WebKit browsers as well as Firefox. However, Internet Explorer did not implement this functionality, and the webSQL standard was soon dropped from the HTML 5 standard itself, leaving only the LocalStorage key/value storage mechanism.

With the advent of the now hugely popular NoSQL databases such as MongoDB as well as Redis and others, the power of a key/value store in the browser has become immensely evident. In addition, with LocalStorage, you can be assured that every major browser supports it, even Internet Explorer 8 and newer. As a result, you would take a look at the [W3Schools](http://www.w3schools.com/html/html5_webstorage.asp) site on LocalStorage and assume that you can do something simple like:

```
if (typeof Storage !== "undefined") {
    localStorage.setItem("key", "value");
}
```

While this will work in all browsers, there are some scenarios that render this check useless. The most important of all to consider is Private Browsing in Safari across all devices and operating systems. It turns out that when you enable Private Browsing in Safari, the `Storage` object is still defined, but when you go to actually use `localStorage` it will throw an exception that will completely derail the rest of the JavaScript on your website. In order to be absolutely sure whether you can use `localStorage` on a particular browser, you should use something similar to the following to detect its availabiliy:

```
var useLocalStorage = false;

try {
    if (typeof Storage !== "undefined") {
        useLocalStorage = true;
        localStorage.setItem("key", "value");
    }
} catch (e) {
    useLocalStorage = false;
}

if (useLocalStorage) {
	// Do your localStorage operations here
}
```