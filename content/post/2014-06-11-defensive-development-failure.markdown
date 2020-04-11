---
date: "2014-06-11T02:11:35Z"
tags:
- javascript
- design-patterns
title: Defensive Development Failure
---

In the past, I have argued that devensive development is a useful tool to ensure unexpected exceptions are not introduced into a piece of software as well as ensuring that the error conditions are handled in an appropriate manner. Unfortunately, if defensive development is implemented poorly, it achieves none of its goals and can cause errors and exceptions to occur. One example that I found while reviewing some code recently is below:

```
var func = function(objParam1) {
	var isValid = true,
    	status;
    if(objParam1 === null) {
    	isValid = false;
        status = "failure";
    }
    if(objParam1.value1 === null) {
    	isValid = false;
        status = "failure 2";
    }
    if(isValid === false) {
    	return status;
    }
    /* Do Stuff Here */
};
```

So, do you see what the problem is here? The issue is that while we are properly detecting that `objParam1` is null, we do not short-circuit the execution of the code, instead allowing it to fall into the check on `objParam1.value1` and whether it is null. However, `null` does not have a member named `value1`. In JavaScript, this would trigger an unhandled exception and prevent the execution of other JavaScript on the page.

The correct way to write the above code in a Defensive Development method would be as follows:

```
var func = function(objParam1) {
    if(objParam1 === null) {
    	return "failure";
    }
    if(objParam1.value1 === null) {
    	return "failure 2";
    }
    /* Do Stuff Here */
};
```

As you can see, this code is much more concise, and fails fast, ensuring the least amount of code is executed as is possible.