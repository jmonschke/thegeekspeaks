---
date: "2014-05-19T14:21:29Z"
tags:
- internet-explorer
- performance
- chrome
- firefox
title: Google Analytics Site Speed is a bit Unreliable
---

Google Analytics will now allow site owners to track the performance of their websites with real live traffic. This is a nice feature that lets you understand just how long it takes for the average visitor to your site to see the fully complete version of your website. While this sounds like a great tool that will give you an accurate view of yoru website's performance, it does not tell the full story. You can access the Site Speed section of Google Analyics under the Behavior>Site Speed>Overview section. Please be aware that not all visitors will send this information, so you will have to have a certain amount of traffic to your site before you will get any information in this section at all.

There are many factors that come into play when you measure the performance of a website. These include but are not limited to:

1. Network Connection
2. Web Browser
3. Computer/Device Performance
4. Screen size/resolution
5. Internet Congestion
6. Web Server Traffic Load

While this is not an exhaustive listing of the factors that come into play, they are a good starting place to outline how they can affect these numbers.

##Network Connection
A User's network connection is the single most important factor to consider when measuring or reading measurements of the performance of your website. If a user is on non-3G wireless or the equivalent of dial-up internet access, it doesn't much matter what you do to optimize your site, if there are any images or any other large assets on the site, it will load slowly. If Google Analytics allowed you to filter the site speed results by connection speed, it would allow you to get a more accurate picture of how the download size affects the visitors to the site, also indicating if your visitors can handle a more image-intensive site, or if a lighter-weight site would be preferred.

##Web Browser
Assuming that we are only discussing the latest and greatest browsers from each of the major vendors, this has very little impact on the performance of your site. However, while Firefox, Chrome, Safari, and Opera have all had adequate performance in their older versions of the browsers, older versions of Internet Explorer, however, had significant performance limitations that would cause websites to load more slowly than the other browsers. Fortunately, Google Analytics shows the differences in performance between Web Browsers.

##Computer/Device Performance
This is another factor that is inconsequential to users of your site that have relatively current computers or devices they use to access your site. However, if a user is using an old and outdated computer or mobile device, they will likely have a worse experience with the performance of your site than what the average user would. 

##Screen Size/Resolution
While this may not seem like a big deal, there are many ways that this can impact the performance of a website. The first is that users that have lower screen sizes or resolutions tend to either be using older mobile devices or older desktop/laptop computers, resulting it lower processing capability to display the site. In addition, if you have a device with a higher resolution, then some newer sites will download higher resolution images to ensure the device gets images that are optimized for the higher resolution. However, this also will increase the total downloaded size for the site, so this will slow the site down as well. While Google Analytics overall allows you to view the screen resolutions of visitors to your site, they do not provide the same information for the site speed portion.

##Internet Congestion
This has become more of a factor with the increase in the amount of streaming media that is available out there with YouTube and Netflix and others. During peak viewing times, it is not unusual for certain sections of the internet to become congested, causing internet traffic to take longer to get to the user than is typically expected. As this is something that happens outside the realm the web browser or your web server, there is not really a way to measure this impact.

##Web Server Traffic Load
While you can hopefully optimize your site so that is able to be served as quickly as possible, there is always a point at which your web servers can take no more traffic without slowing all of the traffic down overall. Once you reach this point, the only way to address the slow down is to add additional servers or a more beefy caching solution. Again, this is something that Google Analytics is unable to show you. However, the reporting and analytics tools on your web server should allow you to detect this scenario. If you are not using something to do this with, a tool like [New Relic](http://www.newrelic.com) will allow you to detect this scenario.