[Source](http://blog.nerdin.ch/2014/07/improved-cordova-android-plugin-api.html "Permalink to Nerd In.Switzerland: Improved Cordova Android plugin API")

# Nerd In.Switzerland: Improved Cordova Android plugin API

#  [Nerd In.Switzerland][1]

## Tuesday, July 8, 2014

###  Improved Cordova Android plugin API

Cordova has a nice API for creating your own plugins. When you need to do something in native code, (for improved speed or security) or need to access some hardware, you can create your own plugin. Our team is concentrating on Android and iOS at the moment and one thing that I noticed is how different the API is between those 2 platforms.  
For instance creating a Echo plugin on iOS that has a method called echo all you need is this:  But the same plugin on Android you'll need:  Now there is a bit of boilerplate here where we get the action and dispatch it to the method. Wouldn't it be nice to just create a method like on iOS? Well with the [android-reflect-plugin][2] you can, it will see if the method exists based on the action and invoke it making your plugin much smaller. All you need to do is declare this plugin as a dependency in your plugin xml:  Then, you extend BasePlugin instead of CordovaPlugin and that it:  Lesser lines = easier to understand.

at  [6:15 AM][3] [ ![][4] ][5]

[Email This][6][BlogThis!][7][Share to Twitter][8][Share to Facebook][9][Share to Pinterest][10]

Labels: [aerogear][11], [cordova][12], [plugins][13]

#### 1 comment: