---
layout: post
title: Improved Cordova Android plugin API
date: '2014-07-08T06:15:00.000-07:00'
author: Erik Jan de Wit
tags:
- aerogear
- plugins
- cordova
modified_time: '2014-07-08T06:15:54.889-07:00'
blogger_id: tag:blogger.com,1999:blog-236071318451058546.post-5049267297453612648
blogger_orig_url: http://blog.nerdin.ch/2014/07/improved-cordova-android-plugin-api.html
---

Cordova has a nice API for creating your own plugins. When you need to do something in native code, (for improved speed or security) or need to access some hardware, you can create your own plugin. Our team is concentrating on Android and iOS at the moment and one thing that I noticed is how different the API is between those 2 platforms.
For instance creating a Echo plugin on iOS that has a method called echo all you need is this:

    - (void)echo:(CDVInvokedUrlCommand*)command
    {
        CDVPluginResult* pluginResult = nil;
        NSString* echo = [command.arguments objectAtIndex:0];

        if (echo != nil && [echo length] > 0) {
            pluginResult = [CDVPluginResult resultWithStatus:CDVCommandStatus_OK messageAsString:echo];
        } else {
            pluginResult = [CDVPluginResult resultWithStatus:CDVCommandStatus_ERROR];
        }

        [self.commandDelegate sendPluginResult:pluginResult callbackId:command.callbackId];
    }

But the same plugin on Android you’ll need:

```java
@Override
public boolean execute(String action, JSONArray args, CallbackContext callbackContext) throws JSONException {
    if ("echo".equals(action)) {
        this.echo(args.getString(0), callbackContext);
        return true;
    }
    return false;  // Returning false results in a "MethodNotFound" error.
}

public void echo(String echo, CallbackContext callbackContext) {
    final PluginResult result;
    if (echo != null && echo.length() > 0) {
        result = new PluginResult(PluginResult.Status.OK, echo);
    } else {
        result = new PluginResult(PluginResult.Status.ERROR);
    }
    
    callbackContext.sendPluginResult(result);
}
```

Now there is a bit of boilerplate here where we get the action and dispatch it to the method. Wouldn’t it be nice to just create a method like on iOS? Well with the android-reflect-plugin you can, it will see if the method exists based on the action and invoke it making your plugin much smaller. All you need to do is declare this plugin as a dependency in your plugin xml:

```xml
<dependency id="org.jboss.aerogear.cordova.android.reflect" url="https://github.com/edewit/aerogear-reflect-cordova.git"/>
```

Then, you extend BasePlugin instead of CordovaPlugin and that it:

```java
public class Echo extends BasePlugin {

public boolean echo(String echo, CallbackContext callbackContext) {
    callbackContext.success(message);
    return true;
}
```