---
author: danfox1982
comments: true
date: 2017-01-11 08:34:30+00:00
layout: post
slug: playing-with-the-actor-model
title: Playing with the Actor Model
tags: [Actors, Coding]
image:
  feature: banner.jpg
---

One of the most well-known patterns for arranging business logic in object-oriented programming is the [domain model](https://martinfowler.com/eaaCatalog/domainModel.html){:target="_blank"}.  Essentially this involves creating a set of classes that contain both data and logic so that an operation on a domain entity always has the correct consequences on other entities, for example in a bank account model, depositing money may cause an increase in the total account value, as well as adding a receipt record or performing a tax calculation.  There may also be further consequences in other [bounded contexts](https://martinfowler.com/bliki/BoundedContext.html){:target="_blank"} such as marketing campaigns for alternative ways of saving money.

I've worked on a few applications using a domain model with varying degrees of success, but in each case I've found that more and more orchestration code appearing in a service layer above the domain model.  This is probably a sign that the domain model and bounded contexts weren't quite right... but it was enough to make me think about alternatives to domain modelling.  I want to make it clear that I do not think that using a domain model is a bad idea, as always in software development [there is no right answer](/2013/10/05/it-depends).

## The Actor Model

I then started learning more about the [actor model](http://www.brianstorti.com/the-actor-model/){:target="_blank"} - this link explains it really well but I'll just highlight a few points here.  It differs from the domain model by focussing on lightweight actors that perform one thing, and do it well - similar to the [single responsibility principle](http://www.oodesign.com/single-responsibility-principle.html){:target="_blank"}.  Communications are handled via queues and mailboxes, which means that concurrency is easier though it is something which needs to be kept in mind (as with every architecture when handling multiple requests).

I wanted to write something which wasn't in the traditional list of examples of such applications (like a library or a bank) so I chose to write an application that can keep score of a frame of snooker.  This means it's full of rules and different scores (total score, break score, foul score etc) for each game.  The application is probably over-architected in a way, but this has really helped with my learning of the actor model.

You can find the source code [here](https://github.com/foxy1982/snooker-scorer-2){:target="_blank"}.  It's written in C# and uses [Akka.NET](http://getakka.net/){:target="_blank"} as the actor framework which is based on the excellent [Akka](http://akka.io/){:target="_blank"} for the JVM (often Scala).  I found Akka.NET to be very close to the Akka implementation, and in fact was able to solve some problems by reading Akka examples as there isn't as much information on the internet about Akka.NET.

## Testing

My experience writing [unit tests for Akka.NET using Akka.TestKit](https://petabridge.com/blog/how-to-unit-test-akkadotnet-actors-akka-testkit/){:target="_blank"} was a bit of a mixed bag.  Simple tests that just poke a message into an actor and check for a response were quite simple, but tests for upstream messages to other actors were a little trickier, as were tests using the `BlackHoleActor`.  More complex tests that needed a `TestProbe` were more problematic, but became easier when I'd finally worked out how to configure the `TestProbe`.

The code has a suite of unit tests with fairly good coverage, along with a [Postman](https://www.getpostman.com/){:target="_blank"} test suite which is a good acceptance test.  I'll cover this in another blog post

## Future work

I've gathered some thoughts into a Github Project [here](https://github.com/foxy1982/snooker-scorer-2/projects/1){:target="_blank"} but want to highlight a couple of the more interesting things:

* It doesn't really make use of the asynchronous nature of the actor model since the interface is a simple HTTP request/response setup.  I'd like to make this async too, but that wasn't the focus of this exercise - the focus was to learn more about Akka.NET.

* It's been deliberately designed down the route of [REST/HATEOAS](https://en.wikipedia.org/wiki/HATEOAS){:target="_blank"} purely so I could see how this technique pans out for the client (not implemented yet).  Effectively it means that some of the "logic" of the application is done in the client by navigating or sending data to resources (such as a POST for a shot being taken).

* It has no [supervisor strategies](http://getakka.net/docs/Supervision){:target="_blank"}... I'd like to shoehorn these in to learn about them as they look really powerful for handling problems and repairing the actor system.

So that's it! A little venture into a big world of actors.  Enjoy!
