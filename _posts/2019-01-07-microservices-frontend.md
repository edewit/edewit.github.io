---
layout: post
title: Microservices Frontends
date: '2019-01-07'
tags:
- micro-services
author: Erik Jan de Wit
---
We've been working on what we call ["the launcher"][1].
For those of you that don't know what "the launcher" is about let me introduce it quickly.
The idea behind "the launcher" is to make it easier for developers to get started building micro services.
It does that by setting you up with a project that is fully configured to be build and deployed on Openshift.
Things like github project, webhooks and build configuration are all created with a push on a button.
Just before the end of the year we introduced a new way to setup said project to make it more customizable.
One thing we added is the possibility to also setup a UI frontend for your microservice.

And that's what I wanted to address in this post.
Because if you want to go truly micro service all the way it makes perfect sense that every micro service has it's own UI.
Otherwise you don't have true independence once a service updates the frontend needs updating as well.
But that does come with some challenges, how does one "mesh" all these separate frontends into one site.
As with any software problem there are many ways to solve this.
One of the ways is to use web components as [explained in this post][2].
This post addresses a lot of good practices, but on a very low level.
Once I have multiple frontends build with react and some build with angular, I want to make sure that I only have to load angular and react once.
Maybe even have something that makes sure I'm not using different versions of frameworks.
Another thing that we need is how to include components that are not part of one specific service and need to be included on many pages.
Equally important, would be a way to make this whole setup easier.

Right now I'm thinking of a service like [Tailor][3], but then with better support for different frameworks.
So that you only include each frameworks once, maybe by having some webpack plugins that help with that.
But it should, in my opinion still be based on web components as that will be supported by all the browsers in the future.

If you have thoughts about this or ideas please let me know in the comments.

[1]: http://developers.redhat.com/launch/
[2]: https://micro-frontends.org/
[3]: https://www.mosaic9.org/
