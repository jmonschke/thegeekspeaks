---
date: "2014-07-15T01:59:49Z"
tags:
- responsive-web-design
- rant
- web-development
title: The Easiest Way to Create A Solution That Works
---

The easiest way to create a solution that works...is to do it right the first time. Yes, this is a bit of a cop-out, but it turns out to be an important factor to keep in mind when you are tempted to come up with a quick and dirty solution for a problem that does not follow established best practices and is likely to have code quality issues later.

I have run across many sections of code that I or other developers have written in the past that we thought were "good enough" at the time it was written, yet, I was revisiting the code because we discovered a bug in it. Many times, this code had an issue that would have been trivial to fix at the time it was written, if it were only found. It seems that as a developer, we tend to find the least sufficient solution that will solve the immediate problem we are experiencing instead of finding an optimal solution that will be easily maintained months and years after it was written.

As a result of having to go back and fix so many trivial errors throughout the codebase, I am working towards being more diligent when it comes to ensuring my code meets all code quality and style guidelines. In addition, for code reviews, I look for a way to gently point out stylistic and code quality issues that don't adhere to team standards, assisting the author with correcting the issues where necessary. My goal is to ensure that I do all I can to avoid being part of shipping more defects in code that is headed to production than defects we are fixing with the code change being shipped.

If we write great code the first time, it keeps us from having to come back and rewrite our code later.