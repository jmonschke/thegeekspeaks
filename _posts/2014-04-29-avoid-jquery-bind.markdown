---
layout: post
title: Avoid jQuery.bind()
date: '2014-04-29 03:58:31'
tags:
- jquery
- javascript
- performance
---

When chasing down performance issues, you never know what kind of problems you will find. I was looking for something that would cause jitter when scrolling on the page. After looking at the custom code that runs on every scroll event, I still had not found a reason for the jitter. Looking at the JavaScript CPU profile when scrolling in Chrome showed that there was an overwhelming majority of the time spent in a function in the Prototype JS library.

On close inspection of Prototype JS, it extends the base Object object with a bind method. While my code uses the `jQuery().on()` method to declare event handlers, we were utilizing a plugin that uses `jQuery().bind()` instead. Adding breakpoints to this code made it obvious that for each scroll event that was fired, Prototype JS was hijacking the event, and running it through its processes instead of jQuery handling it, causing much more CPU usage than is normally expected.

Updating this plugin to use `jQuery().on()` fixed one part of the problem. Unfortunately, this was not the only spot where this plugin had issues. While many know it is a good idea to namespace your JavaScript variables and functions, that is not where the namespacing ends. If you create your own custom events that you are triggering and handling with event handlers, you should also namespace the event names. Without it, a simple triggering of `appear`, which means nothing in jQuery, suddenly triggers events that Prototype and Scriptaculous automatically bind to and execute code when they are fired.

Effectively, you should make sure you only use `jQuery().on()` and always namespace your event names and variables.