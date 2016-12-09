---
layout: post
title: Ignore Whitespace Not Available in BitBucket Pull Requests
date: '2014-07-10 03:29:17'
tags:
- rant
- web-development
---

When looking for an online location to use as the host for source code, many people by default look at [GitHub](http://github.com), as it seems to be the most well-known option out there, and is free for open source projects. However, if you would like your source code to be kept private, or would rather use Mercurial instead of Git, GitHub may not be the place for you. Instead, I would suggest [BitBucket](http://www.bitbucket.org) as your source code repository provider.

However, when working with BitBucket, there is one main issue that comes up uniquely to this site. BitBucket does not support the ability to [ignore whitespace](https://bitbucket.org/site/master/issue/6024/ability-to-ignore-whitespace-changes-in) in the pull request or any other diff tool on the website. When you are refactoring your code, the inability to ignore the meaningless whitespace changes makes it very difficult to do a good job of code reviewing the changes, causing a bit of work thats unnecessary. Hopefully, BitBucket will get the message and actually fix this missing functionality.