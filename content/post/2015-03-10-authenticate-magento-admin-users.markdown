---
date: "2015-03-10T01:23:43Z"
tags:
- web-development
- php
title: Authenticate Magento Admin Users
---

Magento's admin interface allows you to do the vast majority of everything that you would ever want to do to manage your eCommerce website. However, there are times when the rigidity of the framework makes it difficult for developers to appropriately customize a layout.

One of the things that we have done to combat these limitations is to create a new administration section of the website specifically for the use of developers and other advanced administrators of the site. In order to do this as seamlessly as possible, one of the requirements was to enable current admin users to use the same authenticated session across the standard Magento admin and our new custom admin systems.

When looking for the best way to do so, it became obvious that not nearly as many people deal with the admin level session control as do frontend session access control. As a result, here is a snippet of the code that allows you to determine whether the visitor to your custom PHP page has been properly authenticated to your existing Magento admin.

```
require '../app/Mage.php';
Mage::app('admin');

Mage::getSingleton('core/session', array('name'=>'adminhtml'));

if (!Mage::getSingleton('admin/session')->isLoggedIn()) {
    // Redirect the User to the Login page
} else {
    // Do your stuff
}
```