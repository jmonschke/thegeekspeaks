---
layout: post
title: Another Micro-Optimization Provides Useless Results
date: '2015-03-26 03:38:36'
tags:
- javascript
- python
- web-development
- php
---

One of the things to remember about performance optimizations performed in isolation is that their results are rarely representative of real-world performance results. This [article](http://www.itworld.com/article/2901453/no-its-not-always-quicker-to-do-things-in-memory.html) outlines the "findings" of the students at a couple of Canadian universities, and comes to the conclusion that string concatenation in memory is slower than writing the same total number of bytes to disk, one after the other.

>String concatenation is a slow and CPU-heavy operation. It drastically affects Micro-Optimization testing when both algorithms do not utilize it.

If you don't immediately see the issue with the algorithm in which the study is utilizing, it will become apparent shortly. You see, when writing to disk, the students were simply writing X bytes at a time to a location on the disk, moving over, writing more. However, when doing it all in memory, they were implementing string concatenatation. These two operations require vastly different amounts of CPU cycles to complete, adding a variable to the performance equation that was not considered in the evaluation.

If the students were actually comparing disk performance versus memory performance, they should have first created a ramdisk and ran the same code against the ramdisk and the normal filesystem on a hard drive or ssd. By creating the ramdisk, you are able to write to a reserved section of memory using the same codepaths in Java and Python that are used for writing to disk, the only difference being the destination and the drivers for that destination, which is as close as possible to comparing two different storage media.