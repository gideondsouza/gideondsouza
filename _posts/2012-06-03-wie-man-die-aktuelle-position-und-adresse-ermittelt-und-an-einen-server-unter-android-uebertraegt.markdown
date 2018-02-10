---
layout: post
title:  How to get the current location, address and send it to a server on android
tags:
- gps
- android
- java
---

Location services especially on mobile platforms have now become the norm these days. So I'm going to cover the following in the this article:

1. Get the location of the users device (via the NETWORK). This will be latitude and longitude.
2. Reverse-Geo code information from the first step and get an address
3. Send that off to a server via Http GET. (This is typically what you would want to do given a location ;) )


### Getting a location

So first off, how do we get the users current latitude and longitude? There are two options (1) We could use the Network (2) Or the GPS. Somehow, getting a location from the network is quite accurate (I tested it a couple times) and it's fairly fast. Getting a location from the GPS then isn't too difficult.

So in a default Android application you would want to add the following permission in your AndroidManifest.xml :

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

This is if you're using the network, to use the GPS you would need:

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

I have an `AddressActivity.java` and a `main.xml`. My view looks like this:

<img src="http://i.imgur.com/jk5Fczm.jpg?1" alt="My Activity View "/>

The first button gets my location and the code is below. This is pretty straightforward and the snippet is plagiarized straight from the [Android docs here][2]. I have two activity level variables `lat` and `lon`, I store the locations here so I can use them later.

<script src="https://gist.github.com/2864370.js"> </script>

To get a location from the GPS you would just change this line:

    locationManager.requestLocationUpdates(LocationManager.NETWORK_PROVIDER, 0, 0, locationListener);
   
To:

    locationManager.requestLocationUpdates(LocationManager.GPS_PROVIDER, 0, 0, locationListener);

### Getting an Address

The magic for reverse geo-coding comes from the [Geocoder class][3].  You would need the Internet permission in your manifest and this results in an internet call.

    <uses-permission android:name="android.permission.INTERNET"/>

I encapsulate all my geocoder stuff into a `GetAddress()` function which I call from my `btnAddress`. It looks like this:

<script src="https://gist.github.com/2864432.js"> </script>

### Send to the Internet

Now typically when you get this far, you want to send this information off to your server somewhere and then do something useful with it. So the last function `postData()` sends a latitude and longitude to my server. I made little dummy program on AppHabour in ASP.NET-MVC3. It sends the data via GET through a URL.

No doubt you need the INTERNET permission as I described earlier. The code looks like this:

<script src="https://gist.github.com/2864460.js"> </script>

And there you have it!

You can [download a fully runnable project of all this code from here][4].

Hopefully soon I will use an AsyncTask to wrap up all of this code, so it happens asynchronously.

  [1]: /Media/Default/BlogPost/blog/eclipse_mainxml_Design.JPG
  [2]: http://developer.android.com/guide/topics/location/obtaining-user-location.html
  [3]: http://developer.android.com/reference/android/location/Geocoder.html
  [4]: https://www.dropbox.com/s/5qp1rbo44sw1si9/AndroidAddressApp.zip?dl=0
