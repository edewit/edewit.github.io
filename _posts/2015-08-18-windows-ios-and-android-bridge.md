---
layout: post
title: Windows iOS and Android Bridge
date: '2015-08-18T05:52:00.000-07:00'
author: Erik Jan de Wit
tags:
- aerogear
- windows 10
modified_time: '2015-08-18T05:52:04.376-07:00'
blogger_id: tag:blogger.com,1999:blog-236071318451058546.post-1033897216343578290
blogger_orig_url: http://blog.nerdin.ch/2015/08/windows-ios-and-android-bridge.html
---

With the introduction of Windows 10, Microsoft announced that there will support [running iOS and Android applications][1]. Now why Microsoft would try and build something like that is clear, Windows Phone is not getting that much traction and the reason for that is because there aren't that much apps. And developers don't build for Windows Phone because of it's market share a catch 22. So to break this they try to make it less of an effort for developers to publish there apps iOS and Android Apps on Windows Phone.

First the Windows Bridge for iOS (previously called "Project Islandwood"). It consists of a compiler that takes objective-c and compiles it to native Windows and some libraries to implement iOS features on Windows. There is a tool to import a Xcode project into Visual Studio, so clearly the goal of this project is not to run an iOS app on Windows, but to share as much of the code you can and create a new Windows app. For now there is only objective-c support maybe swift will come in the future?

Windows Bridge for Android (previously known as "Project Astoria"). On the Android has a different approach, here you can use your Android IDE and run the app without changing anything. I'm guessing this is because of the open source nature of Android. They have created an bridge on OS level and an compiled Android app can run without changes. If you using Android services like GCM there is a Microsoft library that will convert these calls to Microsoft Services. You connect to your phone with a tool installed into your Android SDK and afterwards `adb` will 'think' you windows phone is an android device (called "emulator-5554 - 4.4.4").

I've tried both of these Bridges with our cookbook examples and I must admit that the Android one is super simple to get started with. I took our [Chuck Norris Jokes][2] app and deployed and run it on android without any changes. When I tried push I had some socket connection problems, but this is still a work in progress.

See it in action   

<iframe src="https://player.vimeo.com/video/136605040?autoplay=1" width="500" height="455" frameborder="0" webkitallowfullscreen="" mozallowfullscreen="" allowfullscreen=""></iframe>

With iOS I had less luck, I could only get the supplied example to work. Seems that not all project types are supported and because, our examples all use the [aerogear libraries][3] as either a framework or a pod the importer created a project that Visual Studio couldn't compile. This project is [open source][4] now, so it will get easier to fix things.

I hope these projects will create a bigger market for Microsoft as I like the new direction the company is heading being more open source and less windows platform focused.

[1]: https://dev.windows.com/en-us/uwp-bridges
[2]: https://github.com/aerogear/aerogear-android-cookbook/tree/master/ChuckNorrisJokes
[3]: https://aerogear.org/
[4]: https://github.com/Microsoft/WinObjC/