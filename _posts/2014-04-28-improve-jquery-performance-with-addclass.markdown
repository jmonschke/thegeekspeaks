---
layout: post
title: Improve jQuery Performance With $().addClass()
date: '2014-04-28 01:23:23'
tags:
- jquery
- performance
---

When looking at things that make a website seem sluggish, you might assume that the most popular JavaScript framework out there always does things in the most efficient manner. However, as I have found, jQuery does not always produce the best performance due to it having to support many different browsers with version 1.x. As a general rule, instead of setting CSS attributes directly on the selected nodes, I prefer to instead add and remove classes on those nodes instead, as it seems to perform much better.

When adding classes to a node, I have typically used the default `$().addClass();` function in jQuery. However, as part of some detailed performance tweaking, I have started to track the runtime of each of the functions. As a result, I found that if you only need to support Internet Explorer 8 or newer, you can cut the execution time in half or less in comparison to the more native JavaScript implementation below. You just need to make sure this is executed before you first call the `$().addClass();` function.

```
(function($) {
        $.fn.addClassPM = function(cls){
            if(typeof cls !== 'undefined'){
                var length = this.length,
                i = 0,
                tokens = cls.split(" "),
                tokenLength = tokens.length,
                j = 0;
                for(;i<length;i+=1){
                    if(this[i].classList){
                        for(;j<tokenLength;j+=1){
                            this[i].classList.add(tokens[j]);
                        }
                    }
                    else{
                        this[i].className+=' '+cls;
                    }
                }
            }
            return this;
        };
    })(jQuery);
  };
```
  
The performance comparison can be seen here: [Adding Classes with jQuery and JavaScript](http://jsperf.com/adding-classes-jquery-and-javascript/3)