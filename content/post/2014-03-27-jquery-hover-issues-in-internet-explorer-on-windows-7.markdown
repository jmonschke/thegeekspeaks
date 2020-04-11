---
date: "2014-03-27T01:45:48Z"
tags:
- internet-explorer
- jquery
- windows-7
title: jQuery.hover Issues in Internet Explorer on Windows 7
---

When creating a new mega-dropdown menu for a site I was working on, I used jQuery's .hover event to trigger which content the menu was displayed. This seemed to work as expected in most browsers that I tested in, except for one, Internet Explorer. Unfortunately, it wasn't even in every instance of Internet Explorer.
##Windows 7
After Windows Vista came out as one of the biggest duds that the world has ever seen, Windows 7 was a ringing success. Windows 7 is an extremely functional and useful Operating System in the vein of Windows XP, but during testing of this website, we found one troubling issue with every version of Internet Explorer we installed on it. When you hovered over the menu and triggered the jQuery.hover() event, Internet Explorer seemingly locked-up for a few seconds, making the entire browser unresponsive. In a stroke of strange luck, I was unable to reproduce this functionality in Internet Explorer on Windows 8 or 8.1, so this is something that only affects the older operating systems. The fix is to replace jQuery.hover() with jQuery(document).on("mouseenter") and call the appropriate function as well.

In a related note, Chrome and Firefox look like they make up about two-thirds of current internet traffic today.