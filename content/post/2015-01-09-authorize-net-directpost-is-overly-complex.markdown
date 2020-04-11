---
date: "2015-01-09T04:14:16Z"
tags:
- magento
- javascript
- security
- authorize-net
title: Authorize.Net Directpost is Overly Complex
---

One of the necessary evils that every ecommerce website that wants to accept credit card transactions must deal with is some sort of payment processing company. It just so happens that Authorize.net is one of the largest payment processors around, and they allow you to choose from a few different ways to integrate their payment processing functionality into your website. One of their ways is via DirectPost, which allows an eCommerce website to process a credit card transaction without the credit card information ever being sent through the website's servers.

While the ability to ensure that no credit card information passes through your website is useful for PCI compliance and the ability to lower the potential losses in the event of a hack like the ones that have affected Sony, Home Depot, and Target among others. The implementation of this payment method is less than ideal, especially if you are utilizing Magento as your eCommerce platform. With Magento, the credit card information is entered into a form that is contained in an iFrame that originates on Authorize.net's servers. Once the order is ready to be submitted, JavaScript triggers the form submission to a completely separate domain with a target on the form of a reloaded iFrame. 

When the response from Authorize.net returns, an error may be displayed for credit card verification issues as well as many other reasons. Unfortunately, due to the nature of this iFrame's content originating in another domain, any attempt via JavaScript to try to inspect what the content is or modify it is blocked by the browser as a part of the browser's cross site scripting, or XSS, protections. As a result, the only way that you know that something is loaded in the iFrame is that you are able to successfully listen for the `onLoad` event for the iFrame and respond to it accordingly.

Many times the response that is rendered in the iFrame contains a redirection URL that redirects the browser to the checkout success page. Other responses will display a standard error message. However, this all relies upon Authorize.Net to be able to successfully validate and authorize the credit card payment information. If there is an error which would typically throw an `HTTP 50X` error and that message is returned to the user's browser, there is no way of knowing what was returned to the iFrame since the JavaScript in the browser is unable to access it. 

Although the DirectPost functionality provided by Authorize.Net holds great promise, there have been reports on Stack Exchange and elsewhere that users regularly have issues with DirectPost, and many developers that have attempted to implement it on their sites have tried and failed, instead turning back to much simpler Credit Card Processing processes.