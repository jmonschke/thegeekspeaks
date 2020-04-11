---
date: "2014-04-06T21:06:00Z"
tags:
- magento
- tier-pricing
title: Saving Products in Magento Deletes Tier Pricing
---

Magento's framework makes many things simple to accomplish when working with the products and categories of your eCommerce website. However, I have found one scenario that doesn't exactly work as expected.
##Tier Pricing in Magento
Magento allows you to setup custom pricing levels based upon the quantity purchased. You set the minimum quantity purchased to enable the lower price when the part is added to the customer's cart. You could see where losing the tiered pricing for an entire catalog of products would be a big deal for a site.
##Saving Products
The way I ran across this issue was to load all of the products for a particular category, remove the a category from the list of categories for the product, and then save the product. When I simply performed these steps, all tiered pricing would disappear. In order to combat this, I tried to load tiered prices for the product before saving, but this only caused database errors on save, as Magento was trying to duplicate the tiered pricing settings. The same happened if I loaded the tiered pricing separately, saved the product, and then add the tiered pricing back to the product before saving it again.
##Properly Saving Category Changes for Products
One of the ways that I was able to find to properly add a product to a category and set the position in the category is to use the following:
```
$cat_api = new Mage_Catalog_Model_Category_Api;
$cat_api->assignProduct($categoryId, $productId, $position);
```

It turns out that the `Mage_Catalog_Model_Category_Api` class also has a function, `removeProduct($categoryId, $productId);` that will properly remove a product from a category programmatically without affecting the tiered pricing configuration for the product. While this does work, you should be aware that modifying products in this manner is not a fast process, and will take quite a while even for a few products.