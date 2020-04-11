---
date: "2014-03-29T02:42:50Z"
tags:
- magento
- varnish
title: 301 Redirecting in Varnish
---

In Magento, you can set your secure and non-secure URLs explicitly. This works as expected in most cases, but can cause some issues when you have to specify full URLs or need to make any AJAX requests. When using the Nexcess Turpentine extension to enable Magento and Varnish to work together and you wish to only support traffic at www.example.com and not example.com, you would need to enable the setting in the Turpentine module to normalize the host.

However, when you have the normalize host setting configured and you visit your Magento site at example.com, assuming you have Apache set to use a 301 redirect to www.example.com, this will not work, and your visitor will be stuck at example.com until they click on any of the links on the site. Fortunately, there is a relatively simple enhancement that needs to be made to the vcl file that handles the redirection entirely within Varnish.
##Varnish 301 Redirect Solution
The solution is to add or modify the vcl_recv and vcl_error functions in your vcl file with what is shown below. Once you restart Varnish, anyone visiting example.com will quickly be redirected to www.example.com, making everything work as expected.

```
sub vcl_recv {
    if (req.http.host == "example.com") {
        set req.http.host = "www.example.com";
        error 750 "http://" + req.http.host + req.url;
    }
}

sub vcl_error {
    if (obj.status == 750) {
        set obj.http.Location = obj.response;
        set obj.status = 301;
        return(deliver);
    }
}
```