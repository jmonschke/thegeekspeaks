---
date: "2014-04-02T00:56:52Z"
tags:
- internet-explorer
title: Can Legacy Internet Explorer Go Away Already?
---

For years, Internet Explorer was a four-letter word around web developers. Recently, Microsoft has stepped up their game when it comes to their web browser. I almost have to pinch myself to make sure I'm not dreaming when I type this, but Internet Explorer 10 and 11 are decent and modern web browsers that many websites don't have to do anything special to support.

However, Internet Explorer 9 and before are another story. The latest compatibility problemn I ran across would be one that is quite confusing to a web developer that has not been around those that have dealt with it before. The symptoms are that CSS rules that you can verify are in your CSS file are not being applied in Internet Explorer, but are applied in Chrome, Safari, Firefox, etc.

It turns out that Internet Explorer 9 and below have an arbitrary limit on the number of CSS selectors that are able to be present in a single CSS file. Now, why there is a limit only on the number of selectors in a file, and not one on the total number of CSS selectors combined in all files. At any rate, the fix is to simply separate out the included CSS files into smaller chunks, and that resolves the issue.