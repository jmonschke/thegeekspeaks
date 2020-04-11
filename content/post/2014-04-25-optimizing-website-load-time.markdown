---
date: "2014-04-25T02:26:35Z"
tags:
- magento
- performance
title: Optimizing Website Load Time
---

Assuming you have already done a few things to improve the page load time of your website, such as using a Varnish caching server, GZipping your content in transit, minifying that same content, and turning on all caching options that Magento or your web platform of choice have available, there is still more you can do. When it comes to website performance, the 80/20 rule definitely applies. 80% of the performance tweaks that you perform will only provide a miniscule improvement to the site load time, while the 20% of things you do make a big difference. Any time I am looking to speed of the performance of a website, I seek those 20% items that give you the biggest bang for your buck.

However, once you have done the easy things above that give the big performance impact, there are still a few things you can do that, while more difficult to implement, still offer performance improvement. 

##Limiting Total Payload Size
The one thing that contributes the most to the perceived performance of your site is the total amount of data and images that must be downloaded to display the webpage. These include, but are not limited to:

* Images
* JavaScript Content
* CSS StyleSheets
* HTML Content

Each type of content can be optimized to be delivered in a more efficient method with varying degrees of dificulty and impact to the final output to the website.

###Images
In curent sites, it seems that images are the one type of content that is growing constantly. As data connections improve, web designers keep wanting better and better quality images for their sites. Fortunately there are a few things you can do to lower the file size of the images.

* Select image quality settings of 85 or below for JPG images.
* Convert all JPG images to Progressive JPGs. While this will yield minor file size savings if any, it will make it appear to the user that the image is loading faster as it loads a low resolution version of the image, and then adds higher resolution to the image in place, making it sharper.
* Optimize JPG images with JPEGMini or JPEGtran. These are tools that losslessly compress your JPG images. 
* Optimize PNG images with PNGCrush. This will losslessly compress the image, but the difference is hard to detect to the casual observer.
* Avoid all bitmap, .tiff, and other non-compressed image formats.

###JavaScript Content
Assuming your site already minifies all of its JavaScript and has compression turned on, the vast majority of the work has been done. However, you can still improve this area of the site. Some sites load all of the JavaScript necessary for the display of the website all at once, making it available for use at any time in the future. This causes the user to experience a longer initial page load time, but after that first load, it is cached in the browser and immediately available for use. Another way to handle this is to utilize script loaders like Require.js, which allow you to only load the modules that you need, when you need them, so that if a user doesn't use a feature of your site, you won't have to download the code to support it.

###CSS StyleSheets
Like the JavaScript, if you minify and compress your CSS, you are most of the way there. However, many sites have unused CSS in their stylesheets, sitting dormant, being downloaded time and again, simply because it is not always easy to track what CSS is needed on a site. One nifty tool that allows you to test this is uncss. It is a Node module and can be installed via NPM, and has several configuation options to customize its output.

###HTML Content
Again, if you follow the basic recommendations to minify and compress your content, this is most of the way there. If, like with JavaScript and CSS, you have portions of your HTML content that are downloaded, but not displayed to the user, removing them from the HTML content will certainly lower the size downloaded. Additionally, if you have many layers of element nesting on the site, removing some nesting layers will lower the download size. Also, the browser will be able to more-quickly render the content as it takes more time to parse and render HTML that has more HTML nodes.