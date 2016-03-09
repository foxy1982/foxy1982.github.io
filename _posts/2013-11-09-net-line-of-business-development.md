---
author: danfox1982
comments: true
date: 2013-11-09 20:36:36+00:00
layout: post
slug: net-line-of-business-development
title: .NET Line of Business Development
wordpress_id: 58
categories:
- Coding
tags:
- .NET
- Coding
image:
  feature: banner.jpg
---

If I was building a new .NET line of business application for an enterprise I would genuinely struggle to pick a UI technology.  I don't consider myself an expert in any particular UI tech, but if I had to choose my area of expertise I'd go for WPF.

But is WPF suitable for a new LOB application that might have a ten , twenty year lifespan?  Microsoft have been relatively quiet on the WPF front over the past year or so, and the release of Windows 8 has clouded the issue further - while Win8 pushes desktops into the app arena the available technologies are XAML-based or HTML+JavaScript.  It's as if Microsoft themselves don't know the best technology for an app.

So if WPF is a sub-optimal choice, what else is there?  Well, there's WinForms... fast development, not the prettiest UI and not always the best to deal with to make sure the business logic stays in a testable place.  It's a viable option but is it going to survive the 20 year lifespan?  Possibly not if the Windows 8 change is a pointer to the future.

Then there's web-based, such as ASP.NET MVC.  I've only dabbled with MVC4 before but I don't feel the development speed is the same with web technologies... instead of one language developers need for WinForms, or two for WPF (they need XAML), it needs a minimum of 3... HTML, JavaScript and a .NET language.  That's a lot for rapid development, and are the benefits of it worth it for in-house applications?  It depends - the ease of deployment is definitely excellent!

So where does that leave us?  It leaves us looking for an easy-to-development, quick to deploy UI technology on the .NET stack.

It leaves us looking for Silverlight.  That's right, Microsoft's forgotten child.

Quick and easy for both development and deployment it was an excellent choice for in-house applications.  But Microsoft's silence on it over the past 2 years(?) means that it's effectively dead.  It always was going to struggle against HTML+JS for the battle on the web, but for in-house development surely it still has a massive role to play?
