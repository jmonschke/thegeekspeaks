---
date: "2014-05-21T01:52:40Z"
tags:
- internet-explorer
- javascript
- chrome
- firefox
title: Window.Open Causes Browser Compatibilty Issues
---

One of the things that always annoys me as a web developer is when native browser functions that are accesible from JavaScript do not share the same function signature. One perfect example of this is the `window.open` function. When you are using non-Microsoft browsers such as Firefox and Chrome, you are able to make a call something like this `window.open(url, 'window name', 'dimensions or other settings');`. The window name parameter is important because it allows you to open multiple links in the same external window/tab. However, when using Internet Explorer, especially Internet Explorer 8 and older, you can only use `window.open(url);`. If you try to use the first type of function call, you get a very ambiguous error message in the browser that doesn't tend to show exactly where the error occurred.

It is safe to say that I will remember that there is something to be wary of when using window.open when multiple browser support is required.