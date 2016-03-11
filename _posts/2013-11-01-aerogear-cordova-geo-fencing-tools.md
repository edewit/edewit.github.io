---
layout: post
title: AeroGear Cordova Geo (fencing) tools
date: '2013-11-01T04:33:00.001-07:00'
author: Erik Jan de Wit
tags:
- aerogear
- plugins
- geofencing
- cordova
modified_time: '2015-02-25T02:28:07.503-08:00'
blogger_id: tag:blogger.com,1999:blog-236071318451058546.post-8203970081804612891
blogger_orig_url: http://blog.nerdin.ch/2013/11/aerogear-cordova-geo-fencing-tools.html
---

![][1] A cool thing about mobile device is that it is _mobile_ it's a computer that you take with you. That is why we developed a Cordova plugin to make geo location inside your Cordova application easier. The first thing we did is to create some Javascript to easily create some maps that are mobile optimised and have some convenient functions for typical use cases. For instance have a map that shows where the device is located and a circle indicating the accuracy of this location:  
You can also add the compass plugin and have a triangle in the center indicating the direction that the device is pointing.   
Or a map set on a location a store for instance and draw a geo fence around for the user to indicate when he wants to be warned that he is close to his store.  
These maps are based on the great [Openlayers][2] project.

In the last example I talked about geo fencing, that is the second part of the plugin. Both Android and iOS support geo fencing and the plugin supports both of these. This is how you can use the geo fencing:   
  

    onDeviceReady: function () {
      var params = {
        callback: 'onGeofenceEvent',
        notifyMessage: '%2$s your home!'
      };

      //register the application to get geofencing events in the onGeofenceEvent function
      geofencing.register(params);
    }

    ...

    //status will have a indicate if the region was entered or left
    function onGeofenceEvent(event) {
        console.log('region event id: ' + event.fid + ' got event with status: ' + event.status);
    }

When your app goes to the background a notification with the notifyMessage is displayed in the notification bar Then to add a region that you would like to monitor do the following:   

    var params = {"fid": 2, "radius": 100, "latitude": 47.351440, "longitude": 8.354737};

    geofencing.addRegion(
      function() {
        console.log("region added");
        },
        function(e) {
          alert(e);
        }, params
    );

Hope you like these features the [source is on github][3]

[1]: https://burnsandmcbride.files.wordpress.com/2012/06/geofence.jpg
[2]: http://openlayers.org/
[3]: https://github.com/edewit/aerogear-geo-cordova