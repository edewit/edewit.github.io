---
layout: post
title: AeroGear Cordova Push Plugin release
date: '2014-08-27T02:17:00.000-07:00'
author: Erik Jan de Wit
tags:
- aerogear
- plugins
- cordova
modified_time: '2014-08-27T02:17:07.761-07:00'
blogger_id: tag:blogger.com,1999:blog-236071318451058546.post-7362150717905439075
blogger_orig_url: http://blog.nerdin.ch/2014/08/aerogear-cordova-push-plugin-release.html
---

### Hi all,

After testing and finding some small issues we are happy to announce that the 1.0.0 version of the Cordova push plugin has been released. Thanks to everyone for testing and making this release happen.

We now have support for background notifications, have a look at the [quickstarts][1] for use of this feature.   

Release Notes - AeroGear Cordova - Version push-1.0.0

##  Bug

* [[AGCORDOVA-26][2]] - When app is in background notifications no longer appear on iOS
* [[AGCORDOVA-28][3]] - Remote Notifications not enabled in generated xcode project

##  Feature Request

* [[AGCORDOVA-10][5]] - Background push notification
* [[AGCORDOVA-27][6]] - Improve callback behaviour documentation

[1]: https://github.com/aerogear/aerogear-push-quickstarts/releases/latest
[2]: https://issues.jboss.org/browse/AGCORDOVA-26
[3]: https://issues.jboss.org/browse/AGCORDOVA-28
[5]: https://issues.jboss.org/browse/AGCORDOVA-10
[6]: https://issues.jboss.org/browse/AGCORDOVA-27