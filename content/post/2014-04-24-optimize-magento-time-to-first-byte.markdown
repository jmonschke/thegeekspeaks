---
date: "2014-04-24T00:41:34Z"
tags:
- magento
- performance
title: Optimize Magento Time To First Byte
---

When looking at the performance of your site, waterfall charts are one of the first places you should investigate. The first thing that is represented on these charts is that the HTML for the website is the first resource that is downloaded every time.

As a result of being the first resource downloaded every time, this is the logical first place to look to improve the performance of your Magento website. There are a few ways to make sure that the page downloads more quickly, and they all involve making sure that the file size is as small as possible. 

##GZip Compression
The first way to make the download size smaller and thus, make sure the HTML of the site downloads faster is to turn on GZip compression on the server. This is typically a setting that can be configured on the web server, and will automatically be used when the client's web browser is able to support it.

##Eliminate Unnecessary Content
Many of the pages that you will find online will have HTML that is not used to display the content on the site. Whether this is due to unnecessary nesting of HTML elements or simply hiding content that is not visible. Remove this from the site, and you will be amazed at how much smaller the download size and time will be reduced.

##Minify HTML
Once you have done all of the above, consider minifying the HTML content of the site. This involves removing all of the duplicate whitespace from the HTML content of the site. The one thing to remember about HTML minification is to make sure to leave any spaces in place that exist between HTML tags as these may be used for layout on the site. In addition, if you have inline JavaScript in the HTML, you should make sure to either not remove the line breaks in this portion of the code, remove comments that begin with `//` or replace all comments that start with `//` with `/* code here */` so that you will not inadvertently comment out your JavaScript.

Each of these solutions are fairly simple to implement in Magento, but requires some testing to make sure that nothing is broken in the process.