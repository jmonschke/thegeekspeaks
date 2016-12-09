---
layout: post
title: Visual Studio 2013 EditorPackage Did Not Load Correctly
date: '2014-09-02 00:53:15'
tags:
- microsoft
- visual-studio
---

One of the things that continually conspires to drive me away from Microsoft products and towards those that are free and open source are the random bugs that pop up from time to time in their incredibly expensive software. The other day, I had to restart my Windows development system and discovered I had an issue when I tried to start Visual Studio 2013. When Visual Studio tried to start and open any files that had been previously open or that I wanted to open for the first time, I got this error message: `The ‘Microsoft.VisualStudio.Editor.Implementation.EditorPackage’ package did not load correctly.`

Evidently, this error is fairly common, and tends to cause issues with the `ComponentModelCache` folder. The solution to get Visual Studio again able to open all types of text code files is to close Visual Studio and rename or delete yoru `ComponentModelCache` folder. This folder is located at `%LOCALAPPDATA%\Microsoft\VisualStudio\12.0`. Please note that you will lose some customizations that you have made to Visual Studio, the most obvious of which is the list of files that you had open for each solution the last time you closed that solution.