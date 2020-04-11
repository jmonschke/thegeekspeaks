---
date: "2014-07-03T03:39:21Z"
tags:
- jquery
- responsive-web-design
- javascript
title: == and === in JavaScript and HTML Input Elements
---

If you read any current information about best practices in JavaScript, you will typically find the following advice somewhere in the list of things to do.
> Always use `===` and `!==` while avoiding `==` and `!=`

While I will never argue against this advice, there are a few things that a developer shoule realize when using `===` and `!==` instead of `==` and `!=`. 

1. `===` and `!==` first do a check of the data type of the two objects you are comparing. JavaScript never forces you to explicitly define the datatype for an object you are creating as it will automatically assign one based on the contents of the object and how it was created.
2. The output of all of the Math functions produce integers or floats as the datatypes for the resultant numbers. For example, `Math.floor(10.39438)` will produce `10`.
3. When retrieving the value of any `select` or `input` or `textarea` is always return as a string. This means that even though the value of the string may be a perfectly good number, it will never match a number data type. For example `"10"` is not equal to `10` when using the `===`.

You should always use `===` and `!==` instead of `==` and `!=`, but you should make sure you understand the datatypes you are dealing with so that your comparison works as expected without any surprises at runtime.