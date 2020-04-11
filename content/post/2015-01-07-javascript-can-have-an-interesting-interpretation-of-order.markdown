---
date: "2015-01-07T02:14:36Z"
tags:
- javascript
- web-development
title: JavaScript Can Have An Interesting Interpretation of Order
---

There is an interesting little quirk with the way in which JavaScript decides which function it should execute next. You see, while the JavaScript engine has a single thread of execution, it creates the illusion of multiple simultaneous processes running at once by utilizing a queue of functions to execute. This means that every time you make a call to a function in your JavaScript, there is no absolute guarantee that it will be the next piece of code run, as there may have been other events triggered that beat your custom function onto the execution queue.

You may be thinking that this is interesting and all, but what does it matter to me? Well, lets take the following snippet of code as an example. 

```
var func1 = function() {
    func2();
    $(form).submit();
},
func2 = function() {
    var iframe = $('<iframe src="blank.html" class="hidden" id="testiframe"></iframe>');
    $("div:last").after(iframe);
    $("#testiframe").on("load", onIframeLoad);
};
```

So, based upon looking at the code above that utilizes some jQuery to make things a bit more straightforward, does the function `onIframeLoad` get run first or does the form get submitted to the server first? Does the function `onIframeLoad` ever get called?

As is the case with many things in the world of JavaScript and Web Development, the answer is that it depends. Lets address the second question first. We cannot be absolutely certain that `onIframeLoad` will ever be called because we are not certain that the `blank.html` file will load after we are able to attache the event handler to the newly created `iframe`. It is possible that there is so much else going on with the JavaScript on the page that `blank.html` will load before we setup the event handler. However unlikely, this is a definite possibility.

As for the first question, it again comes down to a question of timing. Without more knowledge about what exactly is going on with all the other JavaScript on the page and what ever plugins are running in the browser. In general, I would expect `onIframeLoad` to be executed first, but I would not want to base the functioning of my website on that expectation. If you wanted to guarantee that `onIframeLoad` is run and is run before the form is submitted, I would change the above code to something similar to the snippet below, which forces the order to be respected instead of guessing at the order.

```
var func1 = function() {
    func2();
},
func2 = function() {
    $("document.body").on("load", "#testiframe", onIframeLoad);
    var iframe = $('<iframe src="blank.html" class="hidden" id="testiframe"></iframe>');
    $("div:last").after(iframe);
},
onIframeLoad = function() {
    $(form).submit();
};
```