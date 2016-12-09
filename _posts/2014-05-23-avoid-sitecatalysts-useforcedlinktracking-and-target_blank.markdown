---
layout: post
title: Avoid SiteCatalyst's useForcedLinkTracking and target="_blank"
date: '2014-05-23 16:13:36'
tags:
- javascript
- rant
- sitecatalyst
- safari
---

All sites rely upon some third party analytics software to track at the very least the number of visitors to a site. Many sites use Google Analytics, which provide much more information that just the number of visitors. Another option that some of the bigger sites use is Adobe Analytics, aka SiteCatalyst to enable more custom tracking options that are not evident through the Google Analytics interface.

One feature of SiteCatalyst is that it allows you to set an option `useForcedLinkTracking` that will track every link on your site for clicks whether or not you have setup custom tracking for the links or not. Effectively what the code does is create a JavaScript event handler to intercept all click events on the `<a href="http://url.com">Link</a>` hyperlinks. Once they are intercepted, SiteCatalyst sends its tracking information to its servers and then procedes to attempt to make sure that the link functions properly. Unfortunately, in some versions of the SiteCatalyst code, it attempts to create a synthetic click event that works in many cases. However, if you are using Safari with the popup blocker turned on, and a `target="_blank"` in the hyperlink, then it will trigger the popup blocker, which simply ignores the click, and the user sees nothing happen at all. In order to fix it, hopefully the latest version of the SiteCatalyst code will handle it, turn off `useForcedLinkTracking`, or, as the very last resort, convert the `<a />` links to another type of element and use JavaScript to open the new window manually when listening for the click event on the new element. It seems this works all the time, but it will prevent SiteCatalyst from tracking those clicks.
