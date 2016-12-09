---
layout: post
title: Never Explicitly Trust Software Because It Is Open-Source
date: '2015-03-13 02:33:22'
tags:
- magento
- javascript
- web-development
- security
- php
---

One of the major ideas behind open source projects is that allowing anyone that wants to view the source code of a project to be able to do so should make bugs and security weaknesses easy to find. While this did not work so well with OpenSSL and its various bugs that have been exposed recently, I do have an example where it worked extremely well.

Magento is an eCommerce platform that has two separate editions. One is a completely open-source and free as in beer Community edition. The other is a somewhat expensive Enterprise Edition. There is a large community of Magento developers that create extentions, or addons, for these two editions of Magento.

One of these "Magento developers" is a company whose products I'd [never use](http://www.advancedcontentmanager.com/). They create some CMS addon for Magento that has an [evil feature](http://magento.stackexchange.com/questions/59834/any-good-reason-for-a-module-to-be-accessing-global-crypt-key-remotely). Many current extensions "phone home" to the main developer's servers to tell them what sites are using their extensions among other various bits of information. What makes this "open source" extension's "phoning home" so [insidious](http://magento.stackexchange.com/questions/59834/any-good-reason-for-a-module-to-be-accessing-global-crypt-key-remotely) is that part of the information it sends to its developer's servers is the private encryption key that the Magento installation uses to encrypt passwords for users among other things. 

>That's right, an open-source Magento extension is collecting private encryption keys and sending them to the extension developer.

While the "developer" of this extension claims this was all to track unauthorized usage of their extension, the response should not make you feel any better about their bad software. If you look at the [Magento Stack Exchange profile](http://magento.stackexchange.com/users/23195/advanced-content-manager) of the supposed "developer", there is no contact information listed or even a website for the extension. If you dig a bit deeper and look at the developer's website, you will be unable to find any way to contact the developer other than the contact form on the website. This developer does not even give you a hint as to what country they are based in, other than the fact that they are processing payments in Euro. To top it all off, the developer also does not disclose any contact information in the registration of their domain.  They seem quite private and secretive for a company that creates open-source extensions for Magento.

The thing to take from this is that before using any software, including open source software, you should weigh the security risks that the software poses and address them appropriately. In the case of Magento extensions like this one that has the potential to expose customer data, potentially even credit card information, you should have a trusted developer review the entire codebase of any third-party extensions you wish to install on your site. 

>To prevent security breaches, an ounce of prevention is worth a pound of a cure.