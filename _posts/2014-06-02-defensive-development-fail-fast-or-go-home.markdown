---
layout: post
title: Defensive Development - Fail Fast or Go Home
date: '2014-06-02 02:07:32'
tags:
- magento
- javascript
- design-patterns
- management
---

[Defensive Development](http://en.wikipedia.org/wiki/Defensive_programming) is a programming practice that is frequently misunderstood, but is nevertheless a critical practice to follow when working in many environments. I have seen articles written that argue that defensive development simply causes nonsensical null checks to be written, and as a result of seeing people writing bad code defensively, argues that no one should practice defensive development. There are other articles that, like many things in software development, argue that you should always use defensive development for everything.

While I am a propronent of defensive development, like most things, somewhere in the middle of the spectrum is where I would suggest developers fall. What this means for languages like PHP and JavaScript is that when you are writing a function that accepts arguments, you should always check to make sure they are in an acceptible state before acting upon them. For example, if you need to access a member of an array or object, first, make sure that the variable is of the proper type, and that the member of the object exists before trying to access the value of the member. Failure to do so may cause errors that prevent users from interacting with your site, or in the case of PHP errors in a framework like Magento, they may be left staring at a blank white screen.

Once you determine that the parameter passed to your function is not of the correct type, you should immediately signal a failure condition for your site/application to handle the failure in a user-friendly manner. The idea is to figure out that a failue condition exists as quickly as possible and then ensure that you can properly respond to it.

In addition to checking that parameters to functions are valid, you should also check the response values from outside functions that are called to ensure that you get sane return values. 

While checking all of these variables and others have sane values before using them may seem like overkill, frequently in PHP and JavaScript errors that can be found with these techniques would present a bad user experience. Properly handling these situations makes the application to better serve the user experience and inform the user of what is happening so that it can be corrected and an ideal resolution can be reached.