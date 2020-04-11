---
date: "2017-02-03T21:05:23Z"
tags:
- magento
- magento 2
- woocommerce
title: The Magento 2 Learning Curve
---

The learning curve for various products and platforms tends to vary greatly depending on the complexity of the system you are learning. For example, people that understand how to use the internet and communicate online via email or Facebook are generally able to figure out how to work with Twitter without much of an issue. On the other hand, when you are looking at the learning curve for designing airplanes that are able to carry people, it should be much more difficult to understand how to start as compared to starting to use Twitter. (Yes, I know there are people out that think learning to use Twitter is exceedingly difficult, and make paper airplanes all day long.)

When you shift the topic to eCommerce platforms, comparing the learning curve for developers that are starting to work with Magento 1 or Magento 2 as compared to Woocommerce, there is a huge disparity. 

## Magento 1

When I first started working with Magento, it was with version 1.7, and the only official documentation that I could find on the project was geared toward the users of the platform, and not developers looking to extend the platform. However, there was an extensive amount of documentation, of varying degrees of relevance to the current versions, that was being produced by other developers such as Alan Storm that work with Magento on a regular basis. To me, simply implementing a simple module that accomplished something on the site and understanding how and why things worked the way the did was not something that was immediately self evident after following a tutorial on Magento. Instead, it took an extended period of time spent looking at the way others had done things, code reviews, and searching the web for ideas for the ideal way to do various tasks. It seems to me that learning Magento 1 development takes way too long compared to the alternatives.

## Magento 2

One of the best things that the Magento 2 release has delivered to the Magento community of developers is vastly improved developer documentation. In my journey towards learning how to develop with Magento 2, I have found a usefulness present in the official documentation, which was sorely lacking for Magento 1. However, while there are some things that are well documented in the official documentation, I've found that overall the target audience of the documentation is for developers that understand how to develop with Magento 2. As I write this, I realize that I want to clarify that this is more in relation to the tone of the writing of the documentation, and not the depth that each topic is covered, as that is a bit disappointing as well. Magento 2's official documentation takes a very broad approach to covering developing with Magento 2, however, most topics are not covered in enough detail to be extremely useful to experienced Magento 2 developers, and are written assuming a level of knowledge of Magento 2 development that newcomers typically will not have.

When you combine the documentation with the fact that the community has yet to have time to be able to encounter many of the issues that were well documented outside of magento.com for Magento 1, newcomers to Magento 2 development have a massive amount of learning to do before they are able to become productive Magento 2 developers that are able to develop at the same pace that could be achieved with Magento 1.

## Woocommerce

Not long ago, I was working on a project that involved picking a new platform for an ecommerce site, and Woocommerce was one of the options that was considered. I can honestly say that from a developer's perspective that had zero prior experience workign with Woocommerce, the developer documentation is some of the best documentation that I have run across. The act of simply consuming a RESTful API was documented in detail with working cURL examples. In addition, to help developers extend the platform, the Woocommerce team developed several client APIs that allowed you to interact with their API without having to do the work of writing all the glue code. Since Woocommerce is an extension on top of Wordpress, enhancing functionality that was part of Woocommerce was documented well in either location and there was a ton of community documentation around the project. 

## Conclusions

While this sounds like developers would always choose Woocommerce if given the chance, there are some major shortfalls of this solution. At the time of evaluation, all data related to customers, orders, products, and content on the site effectively lives in a single table in the WordPress database. For the majority of small ecommerce websites, this won't have any impact, but for busier sites, it definitely becomes a system design decision that you have to architect your web server setup around. In addition, the built in features were greatly lacking when compared to the feature-set of Magento. One of the things that this site was supposed to handle easily was tiered pricing, so that the more a customer buys of a product, the lower the price per item is. However, Woocommerce didn't handle this functionality natively, requiring multiple extensions to handle it, as opposed to Magento, which does it natively.

It all comes down to evaluating whether your site needs any of the extra functionality that Magento provides out of the box. If you determine that it does, the next step is to figure out if it makes sense to work with developers that have to go through the steep learning curve of Magento 2, or an agency that has already done so and has the billing to prove it, or does adding multiple extensions to Woocommerce and a lower learning curve of WordPress make more financial sense. For some sites, the choice is easily Magento 2, and for others its Woocommerce. From a developer that has worked with Magento 2 a bit, and has only evaluated Woocommerce, it appears that the grass is greener on the other side and working with Woocommerce would be a more pleasurable experience.