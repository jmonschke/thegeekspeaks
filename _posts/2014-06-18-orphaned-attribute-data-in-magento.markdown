---
layout: post
title: Orphaned Attribute Data in Magento
date: '2014-06-18 01:34:27'
tags:
- magento
---

Its always entertaining to look at the source of an application that originates from outside your organization. It frequently highlights ways of using technology I was not familiar with beforehand, and sometimes leaves me shaking my head in disgust. I initially started looking at a relatively new third-party module thinking that I would find some sort of major bug that was causing the issues the site was experiencing, but was surprised to find that was not the case. 

The layered navigation on one of the Magento sites I work with was showing nonsensical layered navigation attributes for the category and products I was viewing. After trying a couple of "quick fixes" we hoped would solve the issue to no avail, I decided a closer look at the Elastic Search module we were using was in order. When I was unable to find any issues with the Elastic Search module, and upgrading it to the latest version made no difference, a different approach was needed. 

In Magento, the layered navigation is powered by the attributes that are relevant for a group of products. Typically, attributes are assigned to products through the use of attribute sets that allow you to assign many attributes at once, simply setting the appropriate settings for each attribute. One of the things that I quickly noticed once I started looking at the attributes and attribute sets is that the non-sensical attributes were not members of the attribute set for the products, and were not visible in Magento's administration screens anywhere. As a result, I started looking more deeply into the database and quickly found that the affected products had data for the attributes that were appearing in the layered navigation but were not part of the attribute set for the product. One thing that all of these attributes had in common is that they had a default value configured and all affected products with the orphaned attributes had the default value configured for the attribute.

While I am only able to speculate about how the data got in this current condition, it appears that the attributes were temporarily part of the wrong attribute sets with the default values, setting the data for the incorrect products. When the attributes were removed from the incorrect attribute sets, it seems that the attribute data was not removed from the products, causing the layered navigation to utilize the extra attribute data for refining the search further. A couple of pure SQL queries was able to quickly remove the extra data, and after a re-index of the Catalog Product Search Data, the layered navigation was again back to normal.