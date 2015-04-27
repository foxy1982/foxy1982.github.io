---
author: danfox1982
comments: true
date: 2014-03-18 22:47:50+00:00
layout: post
slug: the-evolution-of-a-software-developers-code
title: The Evolution of a Software Developer's Code
wordpress_id: 90
categories:
- Coding
tags:
- Coding
- Learning
---

... well the start of that evolution anyway.

I'm still walking along the journey myself so there is much for me to learn - including where it leads me next!  But for now, this is What I've Seen So Far...

**Stage 1 - A List of Steps!**

This is where code is written in a god method - one method effectively contains all the functionality of an application.  It's easy to debug as one step follows the next but it's not very scalable... you'll ht problems very quickly.

**Stage 2 - Many Small Lists of Steps!**

A natural follow on from Stage 1.  The god method is refactored into smaller functions, giving re-use and allowing code to be more readable - but we still have our god object.

**Stage 3 - Objects Exist!**

So now we break the up the god object into smaller objects.  Each object can have a single task (or more accurately, a [single responsibility](http://www.oodesign.com/single-responsibility-principle.html)).  More maintainable, more re-use.  Objects interact more because they need to call another class' methods rather than any solid design behind them.

**Stage 4 - Inheritance Exists!**

Well, I can get even more re-use by abstracting common code away into base classes!  However it's easy at this stage to ignore [Liskov's substitution principle](http://www.oodesign.com/liskov-s-substitution-principle.html), leading to code which is difficult to extend.

**Stage 5 - Composition Is Powerful!**

This builds on the two previous steps.  Firstly, objects can have other objects.  Secondly, inheritance can cause difficulties - hence it's often recommended to [prefer composition over inheritance](http://c2.com/cgi/wiki?CompositionInsteadOfInheritance).



And that's really where I am.  I'm intrigued as to where this journey leads next...
