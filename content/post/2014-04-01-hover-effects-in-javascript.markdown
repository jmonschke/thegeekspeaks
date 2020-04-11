---
date: "2014-04-01T02:16:51Z"
tags:
- javascript
- css
title: Hover Effects in JavaScript?
---

One of the things that can be annoying when looking at someone else's code is when a more complex technology is used to solve a problem that can be handled more simply with another method.

An example of this is when you utilize JavaScript to implement a hover effect on some elements. I know of one scenario when you would need JavaScript to trigger a hover effect, and that would be when you want to trigger the hover effect with a touch event. However, in this case, the elements that would be affected by this hover effect are hidden on any mobile device, so the touch events would be unneeded for this hover effect.

The solution? It is to utilize the `:hover` pseudo-class in the CSS selector and style the elements appropriately instead of adding and removing hover-specific classes. Much simpler, more elegant, and it has been the best-practice for years.