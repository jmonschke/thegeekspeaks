---
layout: post
title: Handling Callbacks with a Depth-First Tree in JavaScript
date: '2015-04-20 01:34:05'
tags:
- javascript
- web-development
- nodejs
---

One of the hardest things to do in JavaScript when working with complex data structures and a callback oriented platform is to know for sure when all of your callbacks have been fully executed. This issue came to light when working with a MongoDB datastore that was being used to store an infinitely-deep nested menu structure. 

This menu structure could be visualized as being a tree. In order to get the all of the needed menu items from this tree, a depth-first traversal of the tree was determined to be the easiest to track. Since I typically try to write the least amount of code possible to solve a problem, I started out with a set of simple callbacks that worked perfectly as long as there was only one menu-item that had any children. As soon as I had multiple children to traverse, the timing of the execution of the final callback happened well before it should have as well as occurring again at the correct time, causing some unexpected results.

I am sure that there are many ways to solve this particular issue that have some elegant algorithmic roots, I am trying to use the simplest method possible. In fact, there is a library that was originally written for use with NodeJS the solves this exact issue. The [async](https://github.com/caolan/async) library allows you to use `async.each(array, iterator, callback);`, which will call the `iterator` function for each member of `array`, and the `iterator` function should handle any necessary processing, calling the `callback` function when complete. If any of the instances of `iterator` throw an error, the other instances are short-circuited. If they all run to completion, the `callback` function passed in will be called only when all have completed successfully, greatly simplifying the logic.

A simple example with Mongo and recursion would be: 

```
function loadMenu(element, index, array, done) {
    menu.model.find().exec().then(function (menus) {
        //Do Stuff Here...
        async.each(menus, loadMenu, done);
    });
}

async.each(menu, loadMenu, done);
```