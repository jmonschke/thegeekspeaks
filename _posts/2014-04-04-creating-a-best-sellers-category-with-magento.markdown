---
layout: post
title: Creating a Best-Sellers Category with Magento
date: '2014-04-04 02:06:35'
tags:
- magento
---

Magento allows you to organize products in categories, and a single product can be a member of quite a few separate categories. As a result, you can create a category that is specifically for your top selling products. You could manually keep track of which products sell the best, either by number of sales completed, or by the actual quantity of each product that were sold. If you want to spend all your time managing this category, then this is the way to go. However, there is a much easier way to manage the products in the category.
##Automatically Add Products to a Category
Adding the top-selling products to your Popular Products category is something that takes a bit of thought and planning before implementing it due to some of the restrictions that Magento places on developers working with products and categories. The flow for doing this would be to first get the list of all products that are currently in the Popular Products. Once we have the list of products currently in the Popular Products category, we can remove all of these products from the category, ensuring we do remove products from the category that are no longer popular. Once the category is emptied, we would need to get the list of product ids for the popular products. Once we have this new list of products, we can add them all to the Popular Products category, set the position of the products in the category, and then view the category page that shows our most popular products.

Unfortunately, there is no direct way to set the position of a product in a category by using either the Product or Category collections. However, you can utilize the Category API, which is used for the web services API, and utilize it to add the product to the category and order it properly. While this works, it is not the most elegant solution.