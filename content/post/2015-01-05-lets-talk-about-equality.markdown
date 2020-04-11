---
date: "2015-01-05T02:33:57Z"
tags:
- javascript
- web-development
title: Let's talk about equality
---

Equality has been a major topic of discussion over the last few weeks. Whenever this topic comes up, I am always suprised how limited many people's knowledge about true equality is. Relax everyone, I am talking about equality operators in JavaScript, and not the topic of national discussion recently.

Thinking back to some interviews I have been a part of recently, it became extremely obvious how little most Front End Web Developers know about the JavaScript equaltiy operators. You got that right, I said "operators" because there are two operators that test for equality between two objects, `==` and `===`.

##`==`

This equality operator, called "double equals" for obvious reasons is the one that you run across frequently in many languages other than JavaScript, and it the only equality operator those other languages utilize. In JavaScript, this equality operator has a two step process that it takes to determine whether the values are equal. It first will check to see if the values are of the same data type. If they are both the same data type, it will do a simple comparison to see if the values are the same, returning `true` if they are, and `false` if they are not the same. However, if the values are not of the same data type, the JavaScript engine will attempt to convert the values into matching data types. If  it is unable to do so, it returns `false`. If it is able to convert the values into matching data types, it will then check to see whether the values are equal, returning `true` if they are and `false` if they are not.

##`===`

This equality operator, called "triple equals" for obvious reasons is the one that you mainly will run across in JavaScript. Whereas the double equals tries to take the values and convert them into matching data types before comparing the values, the triple equals requires that the values be of the same data type as well as have the same value. This is important because it allows developers to perform basic sanity checks on the data that is being used for comparisons. `"1" == 1` would result in `true`, whereas `"1" === 1` would result in `false`. While this is a simple scenario that may not make much different either way, there are situations where this could have unintended consequences. For example, does `"100" == true` return `true` or `false`? If you are used to C++ or other related languages, you might expect it to return `true` since in those languages, any positive integer can represent `true`, and any negative integer can represent `false`, however, in JavaScript, it would return `false`.

There are many other scenarios where you may get unintended results with the `==` equality operator, so the general rule is that you should always use the `===` equality operator and use explicit conversions in your code to make sure that the values are of the same data type. This eliminates the strange variations in browsers and how they interpret their ability to convert data types and values for the `==` operator.
