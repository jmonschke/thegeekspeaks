---
layout: post
title: JavaScript Templating
date: '2014-03-31 01:05:23'
tags:
- javascript
---

Many times it becomes useful to be able to make an AJAX request for some data, insert it into some HTML that is already on the client, and then display it to the user. There are a few ways to implement this, each approach has its benefits and drawbacks.

##String Concatenation

Possibly the simplest way to accomplish the templating in JavaScript is to use simple string concatenation with '+'. This is the approach that I see many newcomers to JavaScript use in their code, as it is the simplest to implement. However, it does have a major drawback in that this method has the worst performance of all, especially in older versions of Internet Explorer. This could be implemented as below:

```
var html = '<div class="' + classname + '">' + content + '</div>;
```

##Array Operations

While this is not as simple as the string concatenation, it makes up for the slight uptick in complexity with the fastest runtime of any of the three solutions. If you are supporting Internet Explorer 7 or below, this is a solution that is able to run in an acceptible amount of time. An example is shown below.

```
var html_array = array();
html_array.push('<div class="');
html_array.push(classname);
html_array.push('">');
html_array.push(content);
html_array.push('</div>');
var html = html_array.join('');
```

##Mustache Templating

While the first two approaches are easy to get started and implemented, using Mustache templates are much easier to maintain as they look and function more like pure HTML. Performance-wise this is not nearly as fast as the Array Operations, but, depending on the actual templating engine you are using, can be much faster than simple string concatenation. An example of a simple Mustache template is shown below:

```
var html_template = '<div class="{{classname}}">{{content}}</div>';
```

In the vast majority of cases, I prefer the Mustache templating approach as it is easy to read and maintain. However, if ultimate performance is required, and I am rendering much of the page in JavaScript, then I would utilize JavaScript Array operations instead.