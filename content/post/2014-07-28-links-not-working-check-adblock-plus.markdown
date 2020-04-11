---
date: "2014-07-28T01:48:07Z"
tags:
- rant
- sitecatalyst
- safari
- adblock-plus
title: Links Not Working? Check AdBlock Plus
---

It turns out that the issues with `useForcedLinkTracking` are not isolated just to Safari's popup blocker. Unfortunately, one of the most popular browser for both Chrome and Firefox, AdBlock Plus is subject to [this issue](https://adblockplus.org/blog/links-not-working-on-a-website-you-can-fix-that) as well. 

One of the things that the AdBlock Plus plugin does is attempt to intercept any and all link traffic to determine whether it was created from an actual mouse click or if it was triggered through JavaScript as part of a marketing campaign. When used on a site with Adobe's SiteCatalyst analytics with `useForcedLinkTracking` turned on and `target="_blank"` set in the hyperlink, you will trigger the issue. If you run into this issue, you can fix it by:

1. Click the Adblock Plus icon on the problematic web page.

2. Choose “Open blockable items” from the menu. 

3. Enter “script” as the search term to list scripts only. Typically, the SiteCatalyst script will have “omniture” somewhere in its name, or it will be called “s_code.js”. 

4. If the corresponding line isn’t red then the script isn’t blocked — you can double-click the line to open the filter assistant and block it. 

5. Make sure to select the first option in the “Look for pattern” section of the filter assistant — you want to block only this one script, not the entire folder.

Once you have done this for a site, the site should start working again immediately while you still have the protections offered by AdBlock Plus on other sites.