---
date: "2017-01-11T00:00:00Z"
tags:
- Magento2
- Magento
- Docker
- macOS
- OSX
title: Magento 2, Docker, and macOS don't mix
---
I was excited when the Docker team launched their better-integrated solution for running Docker containers on OS X this past summer. It allowed our team to switch from using full Vagrant/Virtual Box based virtual machines for local development to a much lighter-weight solution. Compared to the Vagrant setup, Magento 1 seemed to run a bit faster and require fewer resources when running in Docker.

However, when trying to setup a similar environment with Magento 2, the performance numbers didn't quite line up when using a macOS host. I'm sure a little background as to the system setup would make things a bit more clear.

##Docker Container Setup

With the ability to separate each service required to run the site, I split up the web server, database server, PHPFPM processes, and Varnish into isolated Docker Containers. The nginx web server container and the PHPFPM containers each had direct access to the source code for the base Magento installation. All the files needed to run the site were held outside of the Docker containers and on the native filesystem for macOS to facilitate developers' ability to access and edit files in their IDE of choice and use git locally to commit them to source control.

There were a few differences and gotchas to be able to get this setup working properly, but it provided a setup that allows developers to switch between development environments quite easily. However, if the developer is trying to run the site locally to figure out if their changes had the intended effects, it was infuriating to utilize as everything took much longer to respond than it seemed that it should.

In addition to a developer working locally with macOS, a QA/Test environment on a Linux VM was setup running Docker with what should have been lesser resources to the developer workstations, but the site on the QA/Test enviornment out-performed that setup.

##Investigating the issue

In a previous post, I had talked about a couple of tricks to get the Magento 2 unit tests running reliably, and this work is what led to finding the root cause of the strange performance of the development sites. Another aspect of the testing frameworks that Magento 2 comes with is that there is the Magento Functional Testing Framework that uses PHPUnit and Selenium web driver to simulate a real-world user using the Magento website and acts as a type of full end to end integration test. For the unit tests, I was able to run them directly within the Docker containers without any issues, but to be able to automate a real Chrome browser window, I had to run the test runner outside of the Docker setup.

As part of the troubleshooting process to get tests working reliably, I attempted to run the unit test suite outside of Docker on macOS, and it completed its base of almost 22,000 unit tests in under 2 minutes. In all my previous runs inside the Docker container, they averaged just under 12 minutes for full completion. As a bit of curiousity of whether I would see similar results on our Linux test server, I ran the Unit test suite there both inside the Docker container as well as outside. On Linux Host, both inside and outside the Docker container averaged just under 4 minutes total run time. After a bit of looking around for ideas as to what may be a contributing factor to this performance, I ran across a few [bug reports](https://forums.docker.com/t/file-access-in-mounted-volumes-extremely-slow-cpu-bound/8076) that highlighted that mounted Volumes in Docker for macOS had file access times that were much slower than what would be expected natively.

Once I was able to figure out that this was an issue that other Docker users were having, I took a further look at what the unit tests were doing to cause a 6x performance difference in Docker as well as 30 second initial ttfb(time to first byte). While Magento 1 had a large number of files that had to be loaded by the PHP process to be able to satisfy a request, the upgrade/refactoring that the Magento core team undertook for Magento 2 greatly increased the number of files required to be loaded for any single request. As a side note, this seems to greatly simplify the complexity in many of the Controller files and configuration files in Magento 1.

## Solution

Once this cause had been verfied as the root cause of our performance issues, I utilized [HomeBrew](http://brew.sh) to install all the same packages that were setup as Docker containers as native installations on my system and re-installed the site. Afterwards, I was able to get sub 2 second first view page load times as well as sub 700 ms repeat view full page load times. The repeat page load times were not significantly different than what it was originally, but the initial page load time is now drastically faster.

One important thing to note with all this is that if you are running Linux on your development system instead of macOS, or if Docker is able to fix the root issue, you can still take advantage of all the benefits of Docker, but for me, until Docker fixes their performance issues on macOS, I'll be developing with Magento 2 on a native installation.
