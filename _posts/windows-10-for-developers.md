[Source](http://blog.nerdin.ch/2015/07/windows-10-for-developers.html "Permalink to Nerd In.Switzerland: Windows 10 for Developers")

# Nerd In.Switzerland: Windows 10 for Developers

#  [Nerd In.Switzerland][1]

## Friday, July 3, 2015

###  Windows 10 for Developers

It's been a while since Windows 10 started it first preview releases and now the release date is approaching (29 July), it's time for me to find out what it's all about especially from a developers point of view. So the biggest change is going to be that there is no longer a need for 2 different binaries, the same code will run on windows desktop tablet and phone (and even xbox). That means if you want to migrate your app and you have `#if`statements you'll need to change them to run time checks:  
  
And to use this Mobile specific API you'll need to add the Mobile Extension SDK:  
  

![][2]

  

This doesn't mean that your app will no longer run on desktop, so you better get those checks right otherwise you'll get type exceptions. You can still target only Phone if you want to though.

  

Now to get your existing app to compile you'll need to convert it to a Windows 10 project. At the time of writing there isn't a convert tool integrated in Visual Studio 2015 to do this automatically yet. I've found this [power shell script][3] that does a lot of thing automatic, my guess by the time of the release there will be something integrated. There are still some small things to fix around the Package.appxmanifest as they introduced a new namespaces, but it will get you started.

  

After running it most of my really simple apps already ran, the only exception was the oauth2 demo. It heavily uses a now deprecated *AndContinue API. Now I was never fond of this and I'm not sad that it's gone. Picking files and oauth2 authentication is now much simpler. I'll create a branch with an updated version of the aerogear-windows-oauth2 library so that you can test this out.

  

One last thing that is pretty cool in Windows 10 is that the 'metro' apps no longer all start default in full screen. I have a 25.7 inch screen and having no way to have 3 apps open at the same time was really frustrating. But now that has been fixed and the new responsive UI you can make things look good on phone and desktop.

  

With Windows 10 there will be a way to convert iOS and Android apps into Windows Phone apps without a lot of changes, that and being able to run desktop apps on phones might increase the number of apps in the store and attract more customers.

  

All in all I think it's a great step forward and I'll love to see my apps on xbox ;)

at  [3:41 AM][4] [ ![][5] ][6]

[Email This][7][BlogThis!][8][Share to Twitter][9][Share to Facebook][10][Share to Pinterest][11]

Labels: [aerogear][12], [library][13], [windows][14], [windows 10][15]

#### No comments:

#### Post a Comment

[Newer Post][16] [Older Post][17] [Home][1]

Subscribe to: [Post Comments (Atom)][18]

## Blog Archive

* [ ▼  ][19] [ 2015 ][20] (3)
    * [ ►  ][19] [ August ][21] (1)
    * [ ▼  ][19] [ July ][22] (2)
        * [Running Feedhenry AppForms on Windows 8.1][23]
        * [Windows 10 for Developers][24]
* [ ►  ][19] [ 2014 ][25] (7)
    * [ ►  ][19] [ October ][26] (1)
    * [ ►  ][19] [ August ][27] (1)
    * [ ►  ][19] [ July ][28] (2)
    * [ ►  ][19] [ May ][29] (1)
    * [ ►  ][19] [ March ][30] (1)
    * [ ►  ][19] [ January ][31] (1)
* [ ►  ][19] [ 2013 ][32] (5)
    * [ ►  ][19] [ November ][33] (2)
    * [ ►  ][19] [ October ][34] (3)

[ ![][35] ][36]

## Labels

[aerogear][12] (13) [cordova][37] (9) [crypto][38] (1) [feedhenry][39] (1) [forms][40] (1) [geofencing][41] (1) [library][13] (1) [openshift][42] (1) [plugins][43] (9) [windows][14] (2) [windows 10][15] (2)

[ ![][35] ][44]

## About Me

![My Photo][45]

[ Erik Jan de Wit ][46]   

:   

[View my complete profile][46]

[ ![][35] ][47]

| -----|

  |

  |

| ----- |
|

 |

 |

Powered by [Blogger][48].

[ ![][35] ][49]