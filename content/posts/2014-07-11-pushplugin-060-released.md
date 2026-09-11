---
layout: post
title: Pushplugin 0.6.0 released
date: '2014-07-11T03:09:00.000-07:00'
author: Erik Jan de Wit
tags:
- aerogear
- plugins
- cordova
modified_time: '2014-07-11T03:09:28.482-07:00'
blogger_id: tag:blogger.com,1999:blog-236071318451058546.post-6014879853550954341
blogger_orig_url: http://blog.nerdin.ch/2014/07/pushplugin-060-released.html
---

A new version of the push plugin (0.6.0) has been released. It now uses the latest push sdks and has a better test suite. Although we have plans to make the tests even better. The full list of changes is:

### Bug

* [[AGCORDOVA-16][1]] - Should fail gracefully if not configured
* [fix a bug with the foreground/isInline flag][2]
* [fix bug with android not sending cached message][3]

### Feature Request

* [[AGCORDOVA-4][4]] - Use latest aerogear-android-push library (0.2)
* [[AGCORDOVA-5][5]] - Use latest google-play-services
* [[AGCORDOVA-8][6]] - Use Plugin android.support.v4 as dependency rather than adding the jar directly
* [[AGCORDOVA-9][7]] - The example shipped with the plugin should use the latest API (simplification)
* [[AGCORDOVA-11][8]] - Update the underlying iOS Push SDK
* [Automate plugin testing using grunt-cordova-plugin-jasmine.][9]

[1]: https://issues.jboss.org/browse/AGCORDOVA-16
[2]: https://github.com/aerogear/aerogear-pushplugin-cordova/commit/9f1766356d93e223f7678f9e53884e17d82a6467
[3]: https://github.com/aerogear/aerogear-pushplugin-cordova/commit/95db7d91610fdf410b0be544b43ef5bbeb63d749
[4]: https://issues.jboss.org/browse/AGCORDOVA-4
[5]: https://issues.jboss.org/browse/AGCORDOVA-5
[6]: https://issues.jboss.org/browse/AGCORDOVA-8
[7]: https://issues.jboss.org/browse/AGCORDOVA-9
[8]: https://issues.jboss.org/browse/AGCORDOVA-11
[9]: https://github.com/aerogear/aerogear-pushplugin-cordova/commit/c12f287fd40027da68bdb6a062a0ebc37427d6d9
  