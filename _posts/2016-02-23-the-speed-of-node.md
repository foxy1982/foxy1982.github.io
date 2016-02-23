---
author: danfox1982
comments: true
date: 2016-02-23 20:34:30+00:00
layout: post
slug: the-speed-of-node
title: The Speed of Node
categories:
- NodeJS
---

I first started using [NodeJS](http://www.nodejs.org) around a year ago and as the first ever professional(?) JavaScript I'd ever written it was a fairly steep learning curve.  JavaScript is an easy language to code in, but it's a difficult language to write good code in - that's something for another blog post.

On the other hand, one thing that the NodeJS ecosystem is really good at is its flexibility and ability to react to change.  This isn't just about the language itself and the speed with which code (both good and bad!) can be developed - it's also about the online tools that help development (such as the package management system [npm](http://www.npmjs.com), [GitHub](http://www.github.com), [Gitter](http://www.gitter.im) and [CircleCI](http://www.circleci.com)).  They're all designed for fast feedback and collaboration, which is brilliant... and really helped me when I had a problem recently.

There's a great tool called [snyk](http://www.snyk.io) that analyzes packages and will tell you when there is a security vulnerability in your codebase.  This could be caused by the particular version of a package you're using, or it could be a package that's a dependency of a package you're using... or it could be a vulnerability in a package which is a dependency of a dependency of a dependency of a dependency... you get the picture.  In my case, it was because the latest version of my direct dependency was dependent on an older version of something else which had a vulnerability, which wasn't great.  The latest version of the dependency was fine though.

Snyk was set up in our development pipeline to fail an automated build if an issue was detected.  Now this is obviously very conscientious behaviour - shipping code which you know has a security vulnerability doesn't make you feel good.  It's also not really being a Good Internet Citizen.  Unfortunately, it's really frustrating when you want to get the latest feature out into the wild!  Luckily for us, the NodeJS ecosystem and the community sprung into life...

The code with the vulnerability was open sourced in github, making it trivial for us to fork, update the package.json, run the tests and create a pull request.  That was the easy bit - the bit under our control.  Everything else - the acceptance of the pull request and crucially the publishing of the latest version of the package into npm - was out of our hands.  And yet, within hours, people were asking when the fix would be published, and within 2 days the latest version was published and we were free to release our feature.

So all in all, a really, really good, positive experience of being part of a NodeJS community trying to do the right thing.  And I'll be honest, even though similar tools are available - GitHub, [NuGet](http://www.nuget.org) etc - after 10 years of being a .NET developer I'm yet to feel a part of a community in the same way.