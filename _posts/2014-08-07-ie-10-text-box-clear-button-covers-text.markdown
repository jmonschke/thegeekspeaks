---
layout: post
title: IE 10 Text Box Clear Button Covers Text
date: '2014-08-07 02:36:27'
tags:
- internet-explorer
- microsoft
---

When working on a project that required quantities to be entered into a text box and displayed aligned to the right of the text box, I ran across a peculiar issue. If the text box had focus, a new button appeared in the text box that would allow the user to completely clear the contents of the text box. When focus moved to another element on the page, the clear button disappeared, but part of the right side of the text that was previously displayed in the text box disappeared as well. If you were to inspect that element's value via JavaScript, you would discover that the data was still intact, and that only its display was affected.

Unfortunately, the only way to reproduce these symptoms was to view the site in Internet Explorer 10. It seems that [others](http://stackoverflow.com/questions/14007655/remove-ie10s-clear-field-x-button-on-certain-inputs) have had this sort of issue before, entirely in IE10. I have attempted to reproduce the issue with IE11 to no avail as it seems that Microsoft was able to correct this bug before they released the latest version of their browser. There is a [workaround](http://msdn.microsoft.com/en-us/library/windows/apps/hh465740.aspx) that should help hide the text box clear button whether the field has focus or not.

If you want to hide the clear button for all text-boxes, you can use the following CSS, and customize it to fit your needs.

```
input[type="text"]::-ms-clear {
    display: none;
}
```