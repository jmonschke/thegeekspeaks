---
layout: post
title: The Amazing Magento Configuration
date: '2015-03-06 03:17:46'
tags:
- magento
- xml
---

At the heart of every piece of PHP in Magento is the XML configuration files that tell core Magento code where to find functions and what to do with them. It seems to be the biggest hurdle that most developers face when they begin developing with Magento.

When going through a bit of code recently, I discovered something in the configuration that looks like it should have never worked, but amazingly enough, has worked without issue the entire time it has been in place. Let's see if you spot the bit of strangeness.

```
<trans_eamil>
    <ident_customemail>
        <name>Custom Magento Email Address</name>
        <email>custom@email.com</email>
    </ident_customemail>
</trans_eamil>
```

Did you see it? If you didn't notice it right away, `trans_eamil` is misspelt, as it should be `trans_email` instead. Amazingly enough, it seems that Magento completely ignores the node name `trans_eamil` and instead looks for `ident_customemail`, finding it without any issue. 