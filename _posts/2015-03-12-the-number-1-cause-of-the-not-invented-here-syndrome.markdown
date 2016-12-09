---
layout: post
title: The Number 1 Cause of the Not Invented Here Syndrome
date: '2015-03-12 02:44:18'
tags:
- magento
- jquery
- javascript
- web-development
- php
---

One of the quickest ways to get a new internal tool bootstrapped is to utilize an existing design, making slight adjustments to ensure the design matches the requirements of the current project. Instead of using another internal tool as the basis for the new design, I used a design that was purchased specifically for this project. 

This particular design was unique in that there were multiple working examples using AJAX, pure HTML, and AngularJS. While it was nice having supposed working examples, when you start to look at the readme file for how to get this functionality working on your own hosting setup, thats when the niceties disappear. Specifically when lookng at the readme file for AngularJS, it effectively says: "Because this is a well-known JavaScript framework, we are not including any documentation for how it works or how to get started with our design". Granted, the inner workings of AngularJS need not be covered in the readme, but a simple walkthrough of what to expect this design to do would make things much more user/developer friendly.

If you think that this web designer is the only culprit for this type of missing documentation, lets take the major eCommerce platform Magento as an example. While there are many tutorials for the end user to setup and manage their online store, there is very little from the Magento project itself about how to extend Magento's functionality. While there are quite a few blogs, including this one, that appear in search results for how to implement small pieces of functionality in Magento, there is no user-friendly documentation about Magento and how to properly extend it, leading to wildly-varying ideas of what the 'Magento way' of doing something is.

Any seasoned developer will tell you that you can judge the quality of a software project based upon the documentation it provides to other developers that must use or maintain the project long after the original developers are no longer involved. In the two scenarios above, they each offer some extremely nice functionality that is time consuming to replicate, yet they fail to make it as easy as possible for future developers to pick up the project and utilize and extend it. 

As a result, many time the experienced developer's gut reaction to the question of whether you build something yourself or buy it off the shelf is that you should always build it yourself. Either way, there will be defects in the finished product, but with the solution built in-house, at least you have some control over the architecture and maintainability of the solution, easing the burden of resolving issues when they arise.