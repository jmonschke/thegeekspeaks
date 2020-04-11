---
date: "2015-04-06T01:44:34Z"
tags:
- css
- html
- web-development
- compass
title: Write Your Own Compass Mixin
---

As a developer working with CSS, one of the things that I find a bit troubling is the amount of style definitions that I have to repeat over and over to achieve the design I desire. One of the basic tenets of software development is to utilize the *DRY* principle, otherwise known as **D**on't **R**epeat **Y**ourself. Fortunately, when you implement Compass and SASS in your project to generate your CSS, you have a way to avoid copy-paste programming.

Compass adds funtionality to SASS that allows us to create mixins that you can call from anywhere in your `.scss` files, passing in parameters that can be defaulted if not provided. A sample mixin would be similar to the `ellipsis` mixin below, along with its usage.

```
@mixin ellipsis() {
	overflow: hidden;
  	white-space: nowrap;
  	text-overflow: ellipsis;
}
.ellipsis {
  	@include ellipsis;
}
```

While this is nice, and works well, you can add a few things to this `ellipsis` mixin to make sure that it works with a few additional features added in. Lets say we want all text that we are going to have automatically apply an ellipsis to should be blue and underlined. We have a couple of ways of doing it. The first way doesn't take advantage of the power of a mixin. 
```
@mixin ellipsis() {
	overflow: hidden;
  	white-space: nowrap;
  	text-overflow: ellipsis;
}
.ellipsis {
  	@include ellipsis;
    text-decoration: underline;
    color: blue;
}
```

This simply adds the desired styles to the `.ellipsis` class, making sure that it does not apply anywhere else. However, if we decide to make this functionality come with the mixin, then we can easily add those parameters to the call of the mixin like so.

```
@mixin ellipsis($color, $textDecoration) {
	overflow: hidden;
  	white-space: nowrap;
  	text-overflow: ellipsis;
    color: $color;
    text-decoration: $textDecoration;
}
.ellipsis {
  	@include ellipsis(blue, underline);
}
```

This will accomplish what we want, but it does require us to pass in the parameters for the color and whether we want the text underlined or strikethrough, but it makes it more difficult to simply add an ellipsis to text. Instead, we can do the following.

```
@mixin ellipsis($color: black, $textDecoration: none) {
	overflow: hidden;
  	white-space: nowrap;
  	text-overflow: ellipsis;
    color: $color;
    text-decoration: $textDecoration;
}
.ellipsis {
  	@include ellipsis(blue, underline);
}
.ellipsis.noSpecial {
	@include ellipsis;
}
```

Now, we can optionally pass in the color of the text we want and how we want the text decorated, and if we don't want any special decorations at all, we can simply call `@include ellipsis` without passing in any parameters.