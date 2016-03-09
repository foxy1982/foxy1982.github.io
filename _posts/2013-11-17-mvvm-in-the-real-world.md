---
author: danfox1982
comments: true
date: 2013-11-17 18:14:35+00:00
layout: post
slug: mvvm-in-the-real-world
title: MVVM in the real world
wordpress_id: 76
categories:
- Coding
tags:
- .NET
- Coding
- MVVM
image:
  feature: banner.jpg
---

I have a lot of time for MVVM ([http://en.wikipedia.org/wiki/Model_View_ViewModel](http://en.wikipedia.org/wiki/Model_View_ViewModel) for more details!).  I find the abstraction between the visualization of the UI, and the data and commands that support it to be unparalleled (at least in the realms of .NET).  That means I can then fully unit test my view models, and by throwing a little sprinkling of dependency injection the data and commands can also be unit tested against the services that support them (or at least mocks).



The only real drawback I've found with MVVM is that it's difficult to produce a good design for the structure of the viewmodels.  This is particularly troublesome with popup windows.... I always seem to end up modelling my viewmodels around the screens behind them... so a view with a popup window would have a viewmodel with a child viewmodel.  However this seems counter-intuitive to me - the point of the pattern is that I can leave the UI design and experience to people who are far better than me at that kidn of thing (which wouldn't be hard).



Having said that, as I said that's just one drawback.  The power of the WPF framework is harnessed well and you can quickly create some really nice, easy to use applications.  I'm not convinced by the unit testing ability of it though... every time I have created a fully unit-testable viewmodel I've ended up spending more time refactoring the unit tests with each modification, which leads me to believe that although it CAN be unit tested, it doesn't necessarily mean that it SHOULD.  Besides, the main focus of unit testing should always be business logic, which is never in the UI, right? ;-)
