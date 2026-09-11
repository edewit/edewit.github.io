---
layout: post
title: AeroGear Cordova
date: '2013-10-10T06:39:00.002-07:00'
author: Erik Jan de Wit
tags:
- aerogear
- plugins
- cordova
modified_time: '2013-10-10T21:25:07.852-07:00'
blogger_id: tag:blogger.com,1999:blog-236071318451058546.post-1126354836415376120
blogger_orig_url: http://blog.nerdin.ch/2013/10/aerogear-cordova.html
---
We support developers that want to use Cordova to develop mobile apps. We already have a lot of documentation on how to get started with Cordova on our site. Now we've added some specialised plugins to start using AeroGear functionality in a Cordova project. 

* The [OTP (One Time Password) Cordova plugin](https://github.com/aerogear/aerogear-otp-cordova) with integrated barcode scanner

With this plugin you can make your logins much more secure generate a QR code on the server and save the secret on the device and use it to generate a one time password. 

* The [specialised push plugin](https://github.com/aerogear/aerogear-pushplugin-cordova) for easy integration with Unified Push Server

The standard PushPlugin can be used with Unified Push Server as well, but there is a lot of setting up to do and the API is different for Android and iOS. The whole this plugin can because it's using the Unified Push server have a lot simpler unified API

* These plugins work with the Cordova CLI (plugman) so installing and using them is easy. All of them contain a example directory with a minimalistic working demo.
  
Another demo Cordova project that takes an exiting web front-end and creates a native application integrated with push messaging. We are thinking about more things we can do to support your Cordova development and would love to get suggestions on where to put our effort.

Some plugins that we are thinking about are:

* Crypto native storage
* GeoTools Plugin (GeoFencing and Maps)
* Google Wallet Plugin
* Ads Plugin (one that combines iOS and Android)
  
Currently we are focusing our efforts on Android and iOS, but maybe we need to support other platforms as well. Windows Phone comes to mind and maybe even Firfox OS. What platforms are you currently supporting?  