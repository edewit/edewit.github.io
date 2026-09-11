---
layout: post
title: Microservices Frontends
date: '2019-12-18'
tags:
- micro-services
author: Erik Jan de Wit
aliases:
- /2019/12/18/microservices-frontend.html
---
*UPDATE 5 Apr*
added link to the [source of the "stitching layer" layer][3] and it contains links to the other services

The microservices mentioned in my [previous post][1] use the vertx event bus to communicate with each other.
An event bus is of course a great way to separate services and have them coupled loosely.
I've used the same technique for the webcomponents the carousel emits an event for the current photo that is being displayed.

```js
  this.$emit("photoId", this.photos[this.counter].id);
```

A great addition to this project would be to use the vertx client side event bus to listen to the server events and update the state of the components.
That way, when different clients "perform a like" for a specific photo, our view will automatically reflect that.

As mentioned on the [previous post][1] I created a "stitching layer" app that uses react.
Optimally we wouldn't have to do this so we have no coupling at all, in it's simplest form we still would have a index.html that includes all the js code of the services.
But this is an easy first step that works.

This is what the app now looks like, the components marked in red are from the photo service, blue is the like service and finally green is the query service.

![stitching layer ui](/assets/images/posts/2019-12-18-microservices-frontend/stitching-layer-ui.png)

A diagram from what we now have the "stitching layer" is still coupling:

|}

{#diagram language="mermaid" alt="Stitching layer architecture" width=361 height=371 diagramOutputFormat="svg"}
graph TD
    SL[stitching layer]
    SL --> UI1[microservice ui]
    SL --> UI2[microservice ui]
    SL --> UI3[microservice ui]
    UI1 -->|rest| MS1[microservice]
    UI2 -->|rest| MS2[microservice]
    UI3 -->|rest| MS3[microservice]
    MS1 --> DB1[(db)]
    MS2 --> DB2[(db)]
    MS3 --> DB3[(db)]
{/}

{|

There is also a transparent proxy to make our request go to the right microservice:

|}

{#diagram language="mermaid" alt="Transparent proxy routing" width=449 height=301 diagramOutputFormat="svg"}
graph LR
    Page[Page]
    Page -->|/photo| PS[photo-service:8080/photo]
    Page -->|/like| LS[like-service:8081/like]
    Page -->|/query| QS[query-service:8082/query]
{/}

{|

In production we'll have to setup this routing some other / better way.

Second challenge that I bumped into was styling.
When you use webcomponents they use the shadow dom and css styling is local.
The way I fixed that now is by using css variables defined in the webcomponents and then set or overridden in the "stitching layer".
But for a production ready type application you would probably want to make your own [patternfly][2] type project or have some sort of style guide.
Downside of that is that your introducing more coupling, another way is to have shared css vars, but then you are duplicating components.

Next and final thing that we need to think about is server side rendering.
Obviously this is something that we would like to have when we have so may different smaller parts and possible different frameworks.
Server side rendering could potentially also remove the need for a "stitching layer" and when done really well help us with developing these kinds of microservices apps.

One of the conclusions that we can make at this point is, although theoretically we could build all of these frontends in any framework, in practice we would want to minimize the number, as it will increase the size of the initial download.
At a minimum we would have to use the same version of the frameworks.

The [source of the "stitching layer" layer][3] and it contains links to the other services

[1]: /2019/12/16/microservices-frontend/
[2]: https://www.patternfly.org/v4/
[3]: https://github.com/edewit/photo-frontend-common
