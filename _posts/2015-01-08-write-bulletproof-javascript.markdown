---
layout: post
title: Write Bulletproof JavaScript
date: '2015-01-08 03:30:21'
tags:
- jquery
- javascript
- web-development
---

While display issues have long been the bane of a web developer's existence, current web development projects tend to have much more client side interactivity, focusing ever more attention on the reliability and resilience of the JavaScript you write to deliver the complete interactive experience. Many things can cause unexpected errors in your carefully crafted code.

However, there are a few things that you can do to make sure that your site degrades gracefully and still provides a basic level of functionality when something in the browser goes wrong. The following snippet of code illustrates a few best-practices for defining your JavaScript namespaced modules.

```
if(typeof namespace !== "undefined") {
    var namespace = {};
}

namespace.module = (function($) {
    var _privateInit = function() {},
    _privateAction = function() {},
    _hiddenAction = function() {};
    
    return {
        init: _privateInit,
        action: _privateAction
    };
})(jQuery);
```

Let's begin with the first `if` statement. It checks to make sure that the object we are using for our namespacing of all of our modules exists. If it does not exist, it creates it in the global scope here.  This particular piece of code can be reused in each and every module that you create that is part of the same namespace without having to worry about overwriting the `namespace` object.

I am utilizing the Revealing Module pattern here to help isolate any errors or exceptions that may inadvertantly be thrown by my code. If an exception were to be thrown in the global scope, nothing in the global scope that was evaluated after the exception would be evaluated, leaving much of your JavaScript unable to be executed by the browser. Using modules that are narrowly focused on a single piece of functionality help to reduce the damage than an unexpected JavaScript error can cause.

Whenever you get around to actually using your module, `namespace.module`, there are a couple of precautions you should take as well. The first is that you should always call your module as seen in the snippet below. 

```

if(typeof namespace !== "undefined" && typeof namespace.module !== "undefined" && typeof namespace.module.init === "function) {
    namespace.module.init();
}

```

The `if` statement above may be a bit overly protective of the code, making sure that all of the parents of the `init()` function exist and that `namespace.module.init` is actually a function and not a string or another random object before trying to execute it as a function. This also serves the situation where your `namespace.module` is provided in a separate JavaScript file from where it is being called, making us unsure of whether that file was successfully loaded or not. When using the `namespacce.module` in our separate script file, we want to make sure it exists before we attempt to use it so that we prevent any errors from popping up if something happens on the network and the file does not load in time.

If you truly want to write bulletproof JavaScript, you should be checking each function call to internal functions to ensure they exist and if they are in namespaces that the namespaces and modules exist before they are refrenced. Not all JavaScript applications are that sensitive to not ever having an unhandled error, but if yours is, you should do all you can to protect it.