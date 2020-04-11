---
date: "2015-03-25T01:30:30Z"
tags:
- magento
- web-development
- php
title: Verify Magento User Access to Admin Functionality
---

When working with Magento, there will inevitably come a time where you need to manually check to see if the currently logged-in user has access to a specific piece of functionality as defined in the ACL settings. Personally, I have come across this situation more often when creating my own custom modules and their custom permissions, but they can be used to check the permissions of any module.

As is so often the case, [Alan Storm](http://alanstorm.com/magento_acl_authentication) has documented the exact solution for this scenario. Lets say that your ACL configuration is setup as it is below...

```
<?xml version="1.0" encoding="UTF-8"?>
<config>
    <acl>
        <resources>
            <admin>
                <children>
                    <permission1>
                        <title>Permission 1</title>
                        <children>
                            <permission1a>
                                <title>Permission 1 a</title>
                                <children>
                                    <permission1a1>
                                        <title>Permission 1 a 1</title>
                                    </permission1a1>
                                </children>
                            </permission1a>
                        </children>
                    </permission1>
                </children>
            </admin>
        </resources>
    </acl>
</config>
```

If you want to check to see whether the current user has been granted permission1a1, you would write something like the following, which returns a `true` or `false` values.

```
$isAllowed = Mage::getSingleton('admin/session')->isAllowed('permission1/permission1a/permission1a1');
```

As you can see, you have to put the XML node names in the full path for the `isAllowed` function call to work properly. If you don't need to check the leaf node permissions, and only the root node, you could do the following instead.

```
$isAllowed = Mage::getSingleton('admin/session')->isAllowed('permission1');
```

Amazingly, this is one of those scenarios where Magento makes things easy in a non-confusing manner.