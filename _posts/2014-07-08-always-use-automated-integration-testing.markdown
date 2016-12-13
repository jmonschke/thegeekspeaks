---
layout: post
title: Always Use Automated Integration Testing
date: '2014-07-08 02:34:25'
tags:
- javascript
- microsoft
- design-patterns
- teams
- testing
---

QA or Quality Assurance of a software project is often the area of software development that is most neglected. Typically developers avoid software testing like their lives depended on it. While a basic level of testing is required for a single scenario to validate that your code "works", the level of testing that is required to ensure that all users have a good user experience across all targeted platforms is something that a developer seems to think is beneath them.

While there has been much progress made with TDD, or Test Driven Development, and BDD, or Behavior Driven Development, many developers avoid writing even automated testing solutions for the projects they develop. From what I have seen, a developer's attitude toward QA in general is a significant indicator at the skill level of the developer. One thing to point out here is that I am saying skill level, and not experience level as these do not necessarily correlate. Also, when talking about skill level, the skill level I am focusing on is the ability to write easy to understand, maintainable and performant code. For my purposes, I will split developers into two overly general categories.

The first category is made up of developers that strive to understand how their code interacts with the rest of the project before starting development. The developer also is able to communicate exactly what their changes are to the QA team, ensuring they have an adequate understanding of the scope of the change so that it can be thoroughly tested. While QA will inevitably find issues with the code at some point, the developer is appreciative the bug was found before it made it to production, and fixes it promptly for QA's verification.

The second category is made up of developers that are frequently over confident of their development abilities and like to rush in to actual coding before having a full grasp of how their part of the project interacts with the whole. Many times, the QA team gets ineffective communication from these developers, and often the testing plan leaves out major functionality changes.

While everyone wishes they were in the first category and wants all their coworkers to also be in that category, reality sets in and it becomes apparent that we all migrate between these categories quite often. The best and easiest way to combat these forays into the second category is to implement automated integration tests for all code that verify the functionality works as expected. While this will never completely replace the manual QA testing efforts, it will help to raise a red flag when a change has inadvertent effects elsewhere in the codebase.

Developers: communicate well with your QA team and write automated integration tests as much as you possibly can.