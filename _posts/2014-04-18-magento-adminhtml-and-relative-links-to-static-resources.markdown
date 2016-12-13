---
layout: post
title: Magento Adminhtml and Relative Links to Static Resources
date: '2014-04-18 02:34:27'
tags:
- magento
- html
---

Relative links in URLs allow you to only specify the path to an resource that is in the same or subfolder of the current folder. Lets say the current page you are on is `http://example.com/test/` and you want to reference an image at `http://example.com/test/image.jpg`. You could put the full `http://example.com/test/image.jpg` in the src attribute of the img tag, or you could use just `image.jpg` instead. This works well when you are not sure what the directory path is the parent directory of your code. However, it can cause some issues when your code is moved to another location, but some resources are not moved, such as `image.jpg`.
##Magento Adminhtml
Magento's Adminhtml, or administration backend goes through a completely different route in the `app/Mage.php` code to enable you to control the menu, products, and content of your site, among other things. Many eCommerce sites using Magento need some aspect of the administration backend customized to handle the unique workflow for the business. However, there are some occasions where this can cause some unintended consequences.
###Relative Links in Magento
When customizing the administration backend for Magento, there are some cases where you may need to include a third party library to achieve the desired result. One thing that many of these libraries do is reference all of their resources with relative links. If, in the process of including the third party library, you neglect to include the resources referenced in the JavaScript or CSS, then it will cause a 404 error to occur when accessing the resources. 

When you factor in that only the URLs that are configured for the administration backend load the backend code, and all others, including 404 not found errors load the frontend code and error pages to help your users find their way, you may start to see some performance issues. I have seen some sites with two such resources with 404 errors attempt to be loaded on every administration backend page load. Not only does it cause the web server to load all of the frontentd `.phtml` files necessary to display the 404 error page, but it also incurs all the same database access calls that are required as well. When accessing the administration backend of this particular site with the 404 resources included, there is a definite delay in the loading of the page. Simply removing the references to these resources that do not exist or correcting these refereces makes the page load extremely quickly, as one would expect.