---
layout: post
title: 'Simplifying AeroGear Cordova Push Plugin '
date: '2014-03-03T11:31:00.001-08:00'
author: Erik Jan de Wit
tags:
- aerogear
- plugins
- cordova
modified_time: '2014-03-03T11:31:40.581-08:00'
blogger_id: tag:blogger.com,1999:blog-236071318451058546.post-7782403837119350275
blogger_orig_url: http://blog.nerdin.ch/2014/03/simplifying-aerogear-cordova-push-plugin.html
---

<p>The whole idea to create our own Push Plugin was to Simplify things. Because when we use the <a href="https://github.com/aerogear/aerogear-unifiedpush-server">UnifiedPush Server</a> we can do with a lot less platform specific configuration. But after some user feedback I've decided to change the API to make it even simpler to get started and more user friendly. </p><p>The API now looks like this: <script src="https://gist.github.com/edewit/9329332.js"></script>This is already a lot better and a lot less platform specific then the original Push Plugin, but as you can see from the comments there are still a couple of things for android and iOS only. What we found to be common mistake is the configuration of the Event CallBack, because we configure it as a string it's not easy to check and an IDE will not complete it for you. So we decided to fix all of these things making the successCallback the function that is called when push message come in. We also removed options that "badge" and "sound" making them always true, because if you don't want to use them then you can just not send them in your message. </p><p>That leaves us with one thing that we didn't like, the variantID and secret are platform specific, and you need create some logic to use one or the other. So why not build this logic into our plugin, what we ended up with is very neat and clean <script src="https://gist.github.com/edewit/9329642.js"></script></p><p>As you can see the config now contains a section for Android and iOS and a generic section. And because the notification function is now passed as a function pointer the plugin can check to see if it's valid. This will make the plugin a lot simpler to get started with. Right now this is still under development, but it will come to a <a href="http://plugins.cordova.io/#/org.jboss.aerogear.cordova.push">Cordova registry</a> soon. </p>