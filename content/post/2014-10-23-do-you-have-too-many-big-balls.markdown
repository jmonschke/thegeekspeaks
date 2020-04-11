---
date: "2014-10-23T01:43:00Z"
tags:
- management
- agile
- web-development
title: Do you have too many big balls?
---

Managing a software development team can be a difficult task when everything is moving along exactly as expected. When you add in the paradigm shift of [Agile Software Development](http://en.wikipedia.org/wiki/Agile_software_development) with [Scrum](http://en.wikipedia.org/wiki/Scrum_(software_development)), management doesn't always have the same insights into what makes up an efficient use of a development team's time. For the rest of this post, lets assume that we are working with a 2 week sprint, with the first day half-used for sprint planning, and the last day half used for the sprint retrospective.

It seems that the whole world thinks about time in a strictly linear perspective, aka, I did task x from 10:00AM until 11:00AM. While this may work when you are recording events that have occurred in the past, it often does not tell the real story when you are forecasting how much time a particular task or story will take. 

When in a sprint planning session, some managers or scrum masters insist on adding stories or tasks to a sprint until they reach this "magical" amount of story points that the velocity of the team has indicated should be a realistic amount of work for a sprint. Unfortunately, when simply taking the top x tasks off the top of the list of items that are ready to work, failing to take into account the composition of the types and difficulty of those tasks can adversely impact the amount of [story points](http://scrummethodology.com/scrum-effort-estimation-and-story-points/) that can be completed in a sprint. 

Instead of thinking of time as linear, for the purpose of sprint planning, it is helpful to think of time as being a three-dimensional column. A single sprint would be represented by a standard 1 gallon water pitcher, and the stories or tasks to be addressed during the sprint can be represented by balls of various diameters based on the story points assigned each story. Lets assume that the average velocity for the team is 120 story points, and we are using the Fibonnacci sequence (1,2,3,5,8,13,21) as the valid story points for any story in a sprint, and the story point for a story is proportional to the size of the ball representing the story. Now, during sprint planning, the idea is to get as many story points complete during the sprint as possible, which would mean we could either take on 120 of the 1 point stories, 6 of the 21 point stories, or some combination of all sized story points.

>The thing to remember about assigning story points to stories is that they are an approximation of the relative amount of effort required to complete a task. 

If you were to simply add up the number of points you would see that any combination would be equally as desirable as your sum comes up close to the total desired number of story points. However, when you think of a sprint as a pitcher, and stories as balls, it becomes obvious fairly quickly that you will never be able to fill all of the space between the spheres. However, by mixing the sizes of the balls, similar to the way tightly-packed clay soil mixes various particle sizes, you can squeeze out the empty space in the sprint, ultimately allowing the team to complete more story points than their velocity might suggest. 

The thing to remember about assigning story points to stories is that they are an approximation of the relative amount of effort required to complete a task. As a result, the larger the number of story points required to complete a task, the more uncertainty there is in the estimate of the effort required. Thus, when developers run across stories that they are unsure about how to resolve, they should be estimated with a higher number of story points than a similarly scoped story that has less uncertainty. Many times larger stories are assigned 21 points and added into sprints without realizing that that will be a corresponding drop in overall velocity for the sprint due to the added complexity of the high story point story.

In previous positions, management would pressure the development team into including 3 or 4 of the 21 point stories into a single 120 story point sprint, expecting everything to be completed at the end of those two weeks. Unfortunately they did not heed the advice of the team, and were completely shocked when the team did not complete all of the story points for the sprint. 

>The first issue is that in Agile Development, management does not dictate exactly what stories are to be addressed during a given sprint. It should only provide the priority of the tasks, and the development team should resolve stories as times allows in the sprint based upon the priority.

Not to belabor the point, but with these large-effort stories, many times the man-hours to story-point ratio is much higher than it would be for a story with fewer story points simply due to the complexity inherent in the higher point task. An ideal sprint would be loaded with stories of all different story points, with at most 1 or 2 high story point stories per sprint.

