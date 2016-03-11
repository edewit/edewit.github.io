[Source](http://blog.nerdin.ch/2014/01/unified-push-just-got-more-unified.html "Permalink to Nerd In.Switzerland: Unified Push just got more Unified")

# Nerd In.Switzerland: Unified Push just got more Unified

#  [Nerd In.Switzerland][1]

## Wednesday, January 15, 2014

###  Unified Push just got more Unified

You probably know that we have a Unified Push server that enables you to notify multiple clients (e.g. Apple, Android and Web) using the same notification. We have had requests in the past to add Java client. I thought how hard could it be and had a go at it.

So for the web we use [Simple Push][2], that is based on the work that Mozilla did. Our implementation of the [Simple Push server][3] could also enable 'normal' Java clients to receive push notifications. We looked for a Java web socket client library to base this on. And because our Simple Push server is also made in Java I could even reuse code for the protocol.

This is how it works, you connect to the Simple Push server and then register a channel:

This way you could also just use simple push in your Java application without Unified Push, but if you also want to use Unified Push your `RegistrationListener` is a good place to register your endpoint so that it will get called for unified push notifications:

With this [client the Unified Push][4] just got more Unified, try it out and let us know what you think

at  [12:20 AM][5] [ ![][6] ][7]

[Email This][8][BlogThis!][9][Share to Twitter][10][Share to Facebook][11][Share to Pinterest][12]

Labels: [aerogear][13]

#### No comments:

#### Post a Comment

[Newer Post][14] [Older Post][15] [Home][1]

Subscribe to: [Post Comments (Atom)][16]

## Blog Archive

* [ ►  ][17] [ 2015 ][18] (3)
    * [ ►  ][17] [ August ][19] (1)
    * [ ►  ][17] [ July ][20] (2)
* [ ▼  ][17] [ 2014 ][21] (7)
    * [ ►  ][17] [ October ][22] (1)
    * [ ►  ][17] [ August ][23] (1)
    * [ ►  ][17] [ July ][24] (2)
    * [ ►  ][17] [ May ][25] (1)
    * [ ►  ][17] [ March ][26] (1)
    * [ ▼  ][17] [ January ][27] (1)
        * [Unified Push just got more Unified][28]
* [ ►  ][17] [ 2013 ][29] (5)
    * [ ►  ][17] [ November ][30] (2)
    * [ ►  ][17] [ October ][31] (3)

[ ![][32] ][33]

## Labels

[aerogear][13] (13) [cordova][34] (9) [crypto][35] (1) [feedhenry][36] (1) [forms][37] (1) [geofencing][38] (1) [library][39] (1) [openshift][40] (1) [plugins][41] (9) [windows][42] (2) [windows 10][43] (2)

[ ![][32] ][44]

## About Me

![My Photo][45]

[ Erik Jan de Wit ][46]   

:   

[View my complete profile][46]

[ ![][32] ][47]

| -----|

  |

  |

| ----- |
|

 |

 |

Powered by [Blogger][48].

[ ![][32] ][49]