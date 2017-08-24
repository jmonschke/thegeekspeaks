---
title: When Should I Use Magento 2 Helpers?
layout: post
date: '2017-02-06 21:05:23'
author: Jeff Monschke
image: helpers.jpg
tags:
- magento 2
- helper
---
One of the objects that developers familiar with Magento 1 will instantly recognize are helpers. When working with Magento 1, helpers proved to be a special type of object that looked similar in invocation to a singleton, but in reality it was more of a lazy way to share functionality between multiple locations. The main benefit to using a helper in Magento 1 is that it made it easier to access the `__` function for translations and it was directly accessible from the template files `.phtml`. I'm sure many of you can relate to accessing a helper with the familiar `Mage::helper('modulename');`.

There have been a large number of architectural changes in Magento 2, and the helper structure was not spared from the changes. One of the nice things that Magento 2 has done is relax Magento 1's strict enforcement of some naming conventions of PHP files and classes, instead opting to follow the PSR standards, making it easier for developers to apply a single coding style standard across Magento and non-Magento php projects. As a result, you can pretty much put any class in any folder and name it any way you would like, however, just because you *can* do something doesn't mean that you *should* do it. 

One such scenario is implementing helpers in Magento 2. If you look at the [Magento 2 Architectural Layers](http://devdocs.magento.com/guides/v2.1/architecture/archi_perspectives/ALayers_intro.html) documentation, the architecture is split between the following layers:

* Presentation Layer
* Service Layer
* Domain Layer
* Persistence Layer

The Presentation Layer includes all the HTML, CSS, and JavaScript for displaying content to the user as well as the containers and blocks required to do so. The Service Layer is responsible for handling the API as well as service contracts for the dependency injection processes. The Domain Layer is where the vast majority of the business logic for each module lives, and handles all the validation and manipulations for items in the Model folder. The Persistence Layer is responsible for persisting data to the database.

When you look at the 4 major layers in this manner as well as other Magento 2 documentation, it becomes clear that there is no mention of the beloved helper. While you can create classes and objects under the `Helper` folder and refer to it elsewhere, in Magento 2, there is nothing exceedingly special about a helper. 

What should I do in Magento 2 when I would have put something in a helper in Magento 1? Well, it turns out that you really have a couple of options. The first one is to put the logic in a new or existing Model class and move on about your day. A second option would be to create a Helper, but in this case I would make sure that the activities of the helper are purely functional, meaning that it doesn't directly change any data. For many of the things that I would have used a helper for in Magento 1, I have determined that they should be implemented as part of a model at this point, and it seems that decision is helping to clean up the code a bit the more code is written.