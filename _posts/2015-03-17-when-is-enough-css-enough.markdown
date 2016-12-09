---
layout: post
title: When Is Enough CSS Enough?
date: '2015-03-17 02:13:04'
tags:
- internet-explorer
- responsive-web-design
- javascript
- css
- html
- web-development
---

One of the major pushes in web development today is to try to do as much of the styling of a website as is possible from within the CSS of the site. The idea behind this is that when you do so, you remove styling responsibilities from your JavaScript and HTML content, resulting in a much better separation of concerns. The other aspect of this is that CSS styling is typically handled in a more native fashion in the browser as compared to what you can accomplish via Javascript.

This idea is one that has many merits and very few detractors. However, I believe there is at least one wrong way to handle this. As an example, Internet Explorer 9 and before has a limit on the number of CSS selectors that it can apply per stylesheet of [4095](http://support.microsoft.com/en-us/kb/262161). After that, any CSS that appears in the stylesheet is completely ignored by the browser. While this seems like a lot, I know of quite a few sites that have had to specificaly split single stylesheets into multiples to simply get around this limitation.

Recently, I was tasked with taking a website that had been abandoned in mid-development and preparing it for launch as fast as possible. Once I had the basic functionality tested and working properly, I started looking into the details of the styling of the frontend of the site. When I found the main CSS file, I quickly scrolled to the bottom of the file to see how big it was, and was completely shocked. This single CSS file was over 13,000 lines of CSS. Amazingly, this was only one of the several CSS files that were compbined into a single piece of CSS that is delivered to the browser. 

Once all of the CSS files have been combined, they nearly reach half a megabyte in size, more than 50 times the HTML payload of the homepage of the site. You might think that some of the space is taken up by some `data-uri` images, but there are no `data-uri` resources in that giant CSS file.

>Any time your global CSS file is 50x the size of your HTML, you are doing things very wrong.