---
layout: post
title: 'Running Feedhenry AppForms on Windows 8.1 '
date: '2015-07-09T05:39:00.000-07:00'
author: Erik Jan de Wit
tags:
- windows
- forms
- feedhenry
modified_time: '2015-08-17T02:36:02.328-07:00'
blogger_id: tag:blogger.com,1999:blog-236071318451058546.post-3400159542648828804
blogger_orig_url: http://blog.nerdin.ch/2015/07/running-feedhenry-appforms-on-windows-81.html
---
In order to use Feedhenry AppForms on Windows 8.1 we need to build them locally.  Not only that, but you'll need to add a compat script in order to have support for dynamic content. I've created a script that shows all the steps

```bash
# Clone an existing Feedhenry forms app
git clone <Feedhenry forms app>

APP_NAME=forms
# Create a new cordova project using the HTML, CSS and JavaScript of the forms app
cordova create $APP_NAME --copy-from <Feedhenry forms app>/www
cd $APP_NAME
cordova platform add windows

# Install the jscompat to be able to have dynamic content
cd ..
git clone https://github.com/MSOpenTech/winstore-jscompat.git
cp winstore-jscompat/winstore-jscompat.js $APP_NAME/www

# Install the 'default' plugins
cd $APP_NAME
cordova plugin add org.apache.cordova.device 
cordova plugin add org.apache.cordova.network-information 
cordova plugin add org.apache.cordova.battery-status 
cordova plugin add org.apache.cordova.device-motion 
cordova plugin add org.apache.cordova.device-orientation 
cordova plugin add org.apache.cordova.geolocation 
cordova plugin add org.apache.cordova.file 
cordova plugin add org.apache.cordova.camera 
cordova plugin add org.apache.cordova.media 
cordova plugin add org.apache.cordova.media-capture 
cordova plugin add org.apache.cordova.file-transfer 
cordova plugin add org.apache.cordova.dialogs 
cordova plugin add org.apache.cordova.vibration 
cordova plugin add org.apache.cordova.contacts 
cordova plugin add org.apache.cordova.globalization 
cordova plugin add com.feedhenry.plugins.splashscreen 
cordova plugin add org.apache.cordova.inappbrowser 
cordova plugin add org.apache.cordova.console

vim www/index.html
# add <script src="winstore-jscompat.js"></script> into the head of the document
```

And a video that shows the result:

<iframe allowfullscreen="" frameborder="0" height="281" mozallowfullscreen="" src="https://player.vimeo.com/video/130214184" webkitallowfullscreen="" width="500"></iframe>

[Feed Henry windows forms][1] from [Erik Jan][2] on [Vimeo][3].

UPDATE:  
Just checked and verified that the workaround is no longer needed for Windows 10

[1]: https://vimeo.com/130214184
[2]: https://vimeo.com/user33829134
[3]: https://vimeo.com/