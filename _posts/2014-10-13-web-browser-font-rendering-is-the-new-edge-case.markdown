---
layout: post
title: Web Browser Font Rendering is the New Edge Case
date: '2014-10-13 01:48:02'
tags:
- internet-explorer
- chrome
- firefox
- safari
- google
---

In the early days of the web, designers and developers relied upon visitors to the sites they were developing to have their chosen font pre-installed on their computers so that their web browser of choice would be able to properly render the selected font. As quickly became obvious, there is a wide variety of fonts installed across all computers worldwide, so this was not an achievable scenario, especially when print level typography was desired. Unfortunately, at that time, the solution was to put all of the text in an image, ensuring the text would display exactly as the designer had specified, but hiding the same text from search engines and blind users.

As Google put more and more effort into influencing web standards and designers and developers had more input into browser feature sets, one of the features that eventually made it into all the major browsers was support for web fonts, or fonts that are hosted somewhere online, and downloaded only when needed to display the text for websites that required it. This means that you can get your multi-language PT Sans font on any website and browser if  you are a designer.

Unfortunately for developers that must implement these typographical decisions, not all browsers were created equal when it came to how they render the width of the font. In a situation where you must have text spaced equally across the screen, and you are unable to rely upon letter-spacing to space the letters, you can spend hours trying to have a matching design across Safari, Chrome for Windows, Chrome for OS X, Firefox for Windows, Firefox for OS X, and Internet Explorer's various supported versions. When you factor in that for new sites, it is also most likely a responsive design that has 4 major breakpoints, it would not be a surprise to have to have 24 different sets of CSS rules to define how the text should be spaced on the screen.

While browsers have come a long way from the days of Internet Explorer 6 versus Firefox, font rendering in the various browsers is still lagging behind when working with web fonts. As an example, just until recently, Chrome 37, the font rendering for Chrome for Windows was attrocious, with the text looking like it was in a much lower resolution setting than the rest of the screen. Browser makers: you have improved so much about developing websites, lets take it the extra distance and make sure font sizes actually mean something across all the major browsers and rendering engines.