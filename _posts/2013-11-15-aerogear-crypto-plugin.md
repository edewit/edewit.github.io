---
layout: post
title: AeroGear Crypto Plugin
date: '2013-11-15T04:56:00.000-08:00'
author: Erik Jan de Wit
tags:
- aerogear
- crypto
- plugins
- cordova
modified_time: '2013-11-15T04:56:33.050-08:00'
blogger_id: tag:blogger.com,1999:blog-236071318451058546.post-4847237411390466999
blogger_orig_url: http://blog.nerdin.ch/2013/11/aerogear-crypto-plugin.html
---

<p>One of our feature that is nearing completion is crypto. Even though we have Javascript support for this feature, we decided that we would create a Cordova Plugin for this as well. With a Plugin we can use the native libraries and by doing so we add a bit more security and more importantly we improve speed. I've tried to stay as close as possible to the Javascript API, but Cordova demands us to work asynchronous so I've ended up with something that is not exactly the same:  </p><script src="https://gist.github.com/edewit/7466859.js"></script><p>For more information about the features that are coming have a look on the <a href="http://aerogear.org">site</a> and on the <a href="https://github.com/edewit/aerogear-crypto-cordova">plugin github page</a></p><p>Let us know if you like the features so far and what features you would like to see next. </p>