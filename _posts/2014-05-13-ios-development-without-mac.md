---
layout: post
title: iOS development without a mac
date: '2014-05-13T12:22:00.000-07:00'
author: Erik Jan de Wit
tags:
- aerogear
- plugins
- cordova
modified_time: '2014-05-13T12:22:55.831-07:00'
blogger_id: tag:blogger.com,1999:blog-236071318451058546.post-1758947379758923359
blogger_orig_url: http://blog.nerdin.ch/2014/05/ios-development-without-mac.html
---

So as you all know you don't need to know any objective-c to build great looking iOS apps. You can build them using HTML5 and javascript, but you still needed a mac to build it into an app and put it into the Appstore. With the introduction of phonegap build that was over you could build it in the cloud and test it on a device.

This is all good and nice but there are some downsides to this approach. First you'll have to do some tricky things to get the [certificates setup](http://www.iandevlin.com/blog/2012/11/phonegap/building-an-ios-signing-key-for-phonegap-in-windows). And then the build test cycle is slow because you'll need to start a build and get it on the phone each time you change something. Now most of you functionality you can test in your browser, but when you are using plugins testing the use of those needs a device deployment.

With the new ['Phonegap Developer App'](http://app.phonegap.com/) you can have a fast test build cycle again even when you are using plugins. This app comes with all the 'core' plugins installed. Now you can build and test your without generating a native app, this means generating the certificates and building with phonegap build can wait until you are ready to put your app into the store.

That is the last hurdle that you need to take, getting your app into the app store, sadly this is not something that phonegap build can do for you, but there is a service called [app store uploader](http://www.appstoreuploader.com/). Now I must admit I haven't tried it, would be cool if phonegap would add this final part of the puzzle as well.

Here is a little video of it in action:

<iframe width="480" height="270" src="//www.youtube.com/embed/uqrIXFfSjJk" frameborder="0" allowfullscreen=""></iframe>