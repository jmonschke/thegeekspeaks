---
date: "2015-04-01T00:41:48Z"
tags:
- responsive-web-design
- css
- html
- web-development
- compass
title: Using The Ampersand With Compass
---

While much of working with Compass to generate the CSS for your site is straightforward, there are a few ways to use Compass the provide great power, but are not as easy to understand at first glance. This article discusses one such way, hopefully making it easier to understand.

The operator that we will be looking at first is the & operator. The & as part of a selector in Compass allows you to take the entire selector string at a higher nesting level than the & currently resides upon, and replace the & with that selector string. Typically, when this precedes a selector with a space between the & and the selector, it would operate normally as if the & were not present. However, if you remove the space, it allows you to select elements with multiple classes assigned to them as part of a single selector token. 

```
.menu {
	li {
    	width: 100%;
        color: blue;
        &:hover {
        	color: white;
        }
    }
}
```

The above snippet of Compass would be converted to the following CSS.

```
.menu .li {
	width: 100%;
    color: blue;
}
.menu .li:hover {
	color: white;
}
```

While this is a simple usage of the &, there is a much more powerful way to utilize it. That would be to put the & at the end of the selector. This placement causes the complete parent selector chain to be added to the end of the selector. While it may just seem that you would properly nest your selectors instead, there are a few ways that this becomes important. The most impactful reason that I utilize this form of nesting is due to the need to occasionally target specific Modernizr classes that are added to the HTML element. As a result, if I want to check to see whether flexbox is supported in the browser with the above example, it would turn into something like this.

```
.menu {
	li {
    	width: 100%;
        color: blue;
        &:hover {
        	color: white;
        }
        .no-flexbox & {
        	padding: 0 10px;
        }
    }
}
```

The generated CSS would look similar to the following.

```
.menu .li {
	width: 100%;
    color: blue;
}
.menu .li:hover {
	color: white;
}

.no-flexbox .menu .li {
	padding: 0 10px;
}
```