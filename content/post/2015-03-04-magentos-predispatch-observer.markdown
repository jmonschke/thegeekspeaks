---
date: "2015-03-04T03:10:36Z"
tags:
- magento
- php
title: Magento's preDispatch Observer
---

One of the decisions that always seems to arise when adding functionality to a Magento website is what the best strategy is for doing so. Should you override the controller or function, edit it in place, or use an observer to listen for a particular event to occur.

It just so happens that if you want to make sure that you have some sort of validation logic that runs before a particular controller action is executed, the easiest way to implement it is via a preDispatch observer. The other aspect of preDispatch controllers is that they can be configured to listen only for preDispatch events from a particular module, or they can listen for preDispatch events from every module, allowing you to add some password expiration policies to the adminhtml side of your website, for example.

To get started, you will need to update your module's config.xml file to include a section like is shown below:

```
<global>
    <events>
        <controller_action_predispatch_routename_product_view>
            <observers>
                <yourmodule_capcpv>
                    <class>YourCompany_YourModule_Model_Observer</class>
                    <method>catalogProductViewPredispatch</method>
                </yourmodule_capcpv>
            </observers>
        </controller_action_predispatch_routename_product_view>
    </events>
</global>
```

The important thing to notice above is that this will only listen to preDispatch events for the `/routename/product/view` controller address. In addition, it will call the `catalogProductViewPreDispatch` function on the `YourCompany_YourModule_Model_Observer` class. This also requires that you have a file named `Observer.php` in the `app/code/local/YourCompany/YourModule/Model` folder.

Once you have this setup, you are able to perform any action you would like to in the observer function. One thing to note is that if you would like to make sure that the `/routename/product/view` controller action is never executed, you can simply make a call to `exit()` within the `catalogProductViewPredispatch` function. It is a messy and inelegant way to accomplish this, but it works without issue.