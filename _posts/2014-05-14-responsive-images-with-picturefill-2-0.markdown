---
layout: post
title: Responsive Images with Picturefill 2.0
date: '2014-05-14 02:09:53'
tags:
- responsive-web-design
- javascript
- performance
---

Responsive Web Design seems to be the way that the majority of websites will be developed in the near future. For a while, everyone was creating a separate website that catered to mobile devices in addition to the main website that desktop browsers were able to access. Web Developers and UX Designers quickly discovered that this was a less than ideal approach as it required maintaining two separate websites, and the mobile website tended to remove data that was visible on the desktop version of the site. 

HTML 5 has allowed Web Developers to be a bit more efficient at optimizing the web browsing experience for visitors of all display resolutions. With Responsive Web Design, current browsers allow you to customize non-image elements with CSS Media Queries. Unfortunately up until recently, there was not a standardized way to handle responsive images such that a device with a 320x480 screen does not receive an image that is 1200x600, but instead receives a smaller version of the image.

The first rule of website performance is to limit the number of bytes that must be downloaded to display the website. Thankfully, the `<picture>` element has been somewhat standardized and is starting to be implemented in Chrome and Firefox, while Internet Explorer continues to lag behind in new functionality implementation. However, there is a working polyfill for the `<picture>` element that works with all major browsers. The [Picturefill](http://scottjehl.github.io/picturefill/) polyfill is the major polyfill out there that is known to work across browsers and is supported by the Filament Group. Using this polyfill simply requires the developer to add the script to the head of the html, and make sure the `<picture>` elements adhere to the standard and a slight workaround for IE9.

Images tend to make up the majority of the download size for any website and this will allow web developers to limit the image sizes that will be downloaded by clients. Take this polyfill and experiment with it and start utilizing Responsive Images today.