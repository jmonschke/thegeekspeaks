---
layout: post
title: Always Namespace Variable Names in JavaScript
date: '2014-04-30 01:59:49'
tags:
- javascript
- design-patterns
---

After running into a few issues with variable naming collisions over the past few days, it drives home how much we all should be namespacing our variable names in JavaScript. When writing JavaScript code that is only in use on your own website, you should still always namespace your variables. If you are writting a JavaScript library that will be in use on any website a user puts it on, namespacing your variable names is a minimum requirement.

In addition, if you are writing a library that extends built-in objects, such as the way Prototype JS does with the Object object, it is extremely important that you namespace the methods and properties you add to the built-in objects. Prototype JS adds a .bind() method to the Object object, which is not a problem until you also include jQuery on the page, which also has a `jQuery().bind()` method. However, now that jQuery recommends that you use `jQuery().on()` instead, it is not as much of an issue, but if you have legacy jQuery sticking around, it can cause some interesting performance issues that are hard to pin down.

In order to namespace variable and method names in JavaScript, there are a couple of ways to implement it.

1. Create a separate object, and make all methods and properties as methods and properties on the separate object. This can be done as below where tgsn is the namespaced variable object.
```
tgsn = {
		property1: 123, 
    	method2:function() {
    		alert("method");
        }
}
```

2. Add a prefix to the name of every property and method that you use.
```
var tgsnProperty = 123,
	tgsnMethod = function() {
		alert("method");
};
```

Either of these two methods will work whether it is a stand-alone object or are extending built-in objects. 