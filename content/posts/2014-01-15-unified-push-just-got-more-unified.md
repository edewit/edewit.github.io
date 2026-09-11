---
layout: post
title: Unified Push just got more Unified
date: '2014-01-15T00:20:00.000-08:00'
author: Erik Jan de Wit
tags:
- aerogear
modified_time: '2014-01-15T07:05:13.490-08:00'
blogger_id: tag:blogger.com,1999:blog-236071318451058546.post-7324958872607277349
blogger_orig_url: http://blog.nerdin.ch/2014/01/unified-push-just-got-more-unified.html
---

You probably know that we have a Unified Push server that enables you to notify multiple clients (e.g. Apple, Android and Web) using the same notification. We have had requests in the past to add Java client. I thought how hard could it be and had a go at it.

So for the web we use [Simple Push][1], that is based on the work that Mozilla did. Our implementation of the [Simple Push server][2] could also enable 'normal' Java clients to receive push notifications. We looked for a Java web socket client library to base this on. And because our Simple Push server is also made in Java I could even reuse code for the protocol.

This is how it works, you connect to the Simple Push server and then register a channel:

```java
  SimplePushClient client = new SimplePushClient("ws://localhost:7777/simplepush/websocket");
  client.connect();
  client.register(new RegistrationListener() {
    @Override
    public void onRegistered(String channelId, String simplePushEndPoint) {
    }
  });
```

This way you could also just use simple push in your Java application without Unified Push, but if you also want to use Unified Push your `RegistrationListener` is a good place to register your endpoint so that it will get called for unified push notifications:

```java
...

  public void onRegistered(String channelId, String simplePushEndPoint) {
      final PushConfig config = new PushConfig();
      config.setDeviceToken(channelId);
      config.setSimplePushEndpoint(simplePushEndPoint);

      unifiedPushClient.register(config);
  }
```

With this [client the Unified Push][3] just got more Unified, try it out and let us know what you think

[1]: https://developer.mozilla.org/en-US/docs/WebAPI/Simple_Push
[2]: https://github.com/aerogear/aerogear-simplepush-server/
[3]: https://github.com/aerogear/aerogear-simplepush-java-client