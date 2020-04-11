---
date: "2014-03-30T02:30:43Z"
tags:
- magento
- varnish
title: Login Problems with Magento and Varnish
---

When you have a Magento website configured to use Varnish as a caching frontend, there are certain scenarios where you may have some problems logging-in to the frontend of the website. It poses some unique problems that are not frequently seen on a typical website. This issue typically manifests itself to the end user by visiting the login page, entering the correct credential, submitting the form, and then the page reloads the login page again instead of redirecting to the My Account page or whatever page is specified in the configuration.
##Diagnosing the issue
So, it is quite interesting to see this happen as the user will still get notified that they are using the wrong username/password combination, but are unable to successfully authenticate with the website. In order for this issue to crop up, you have to have your site setup to use a particular domain, say www.example.com and have a redirect setup so that example.com redirects to www.example.com. Once the user experiences this issue, when you go into the developer tools in the browser, and investigate the cookies in place, you will notice that there are two cookies named "frontend". However, these cookies have two different paths for them. One will be for example.com and the other will be for www.example.com.
##Recreating the issue
It seems difficult to recreate this issue up until the point that you actually do it, and then it becomes trivial. First, go to www.example.com and try to login to the site. Next, logout of the site. After that, visit example.com and try to login to the site. When you submit the login form, it will just refresh the login page without showing any error on the site.
##Resolving the Login Problems
This issue asserts itself when you utilize the Turpentine plugin from Nexcess to enable the proper caching configurations due to Magento's reliance upon cookies being sent with every request. In the configuration of Turpentine, there is a special setting that allows Varnish to normalize the hostname that it requests from the server. Effectively what this will do for you is to take any request that hits Varnish, and translate it to whatever is specified, in this case, www.example.com. In most cases, this works great, and it fixes the login issues described in this article. However, it can create some other issues, specifically with [301 redirects](http://thegeekspeaks.net/301-redirecting-in-varnish/). Overall, once both fixes are in place, everything should work beautifully, and much faster than it did previously.