---
layout: post
title:  Wie man für Android die aktuelle Position ortet, adressiert und an einen Server sendet
tags:
- gps
- android
- java
---

Ortungsdienste sind vor allem für mobile Plattformen zur Norm geworden. In diesem Artikel geht es deshalb um folgende Themen:

1. Ortung des Endbenutzer-Gerätes (users device) über das Netzwerk, also mittels der Ermittlung von Latitude und Longitude.
2. Umkehrung der Geokodeinformation aus Schritt 1. und darüber die Ermittlung der Adresse
3. Senden mittels Http Get. an einen Server (Das ist ja typischer Weise was man mit der ermittelten Ortung anstellen möchte ;) )


### Die Ortung

Wie bekommen wir also zunächst die aktuelle Latitude (Höhengrad) und Longitude (Breitengrad) eines Users? Dafür gibt es zwei Optionen: (1) Wir können dafür auf das Netzwerk zugreifen (2) oder auf das GPS. Dabei scheint die Ortung über das Netzwerk ziemlich präzise Resultate zu liefern (ich habs ein paar Mal ausprobiert) und arbeitet gleichzeitig recht schnell. Eine Ortung vom GPS zu bekommen ist danach nicht besonders schwierig.

In einer Standart-Android-Anwendung muss die folgende Erlaubnis (permission) in die AndroidManifest.xml geschrieben werden:

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Wenn Du die das Netzwerk benutzten möchtest, dann benötigst du zum nutzen des GPS das hier:

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

Hier habe ich eine `AddressActivity.java` und `main.xml`. Das sieht bei mir dann so aus:

<img src="http://i.imgur.com/jk5Fczm.jpg?1" alt="My Activity View "/>

Der erste Knopf gibt mir meinen Standort zurück, den entsprechendnen Code dazu habe ich unten aufgeführt. Die Herangehensweise ist recht einfach und den Auszug habe ich von [Android docs here][2] abgekupfert. Ich habe zwei "activity level variables" "lat" and "lon". Darin speichere ich die Koordinaten um sie später verwenden zu können.

<script src="https://gist.github.com/2864370.js"> </script>

Um eine Ortung über das GPS zu ermitteln muss nur dieser Ausdruck (line) geändet werden. Diese line:

    locationManager.requestLocationUpdates(LocationManager.NETWORK_PROVIDER, 0, 0, locationListener);
   
wird zu:

    locationManager.requestLocationUpdates(LocationManager.GPS_PROVIDER, 0, 0, locationListener);

### Eine Adresse ermitteln

Die Magie des umgekehrten Geo-codings kommt aus der [Geocoder Klasse][3].  Dafür benötigst du die Interneterlaubnis (permission) im manifest und das ermöglicht einen Internetaufruf.

    <uses-permission android:name="android.permission.INTERNET"/>

Ich habe meinen ganzen geocoder-Krempel in eine `GetAddress()` -Funktion gepackt welche ich von meiner `btnAddress` aufrufe. Das sieht dann so aus:

<script src="https://gist.github.com/2864432.js"> </script>

### An das Internet senden

An dieser Stelle würde man jetzt typischer Weise diese Informationen an einen Server senden um damit etwas sinnvolles anzustellen. Dafür sendet die letzte Funktion `postData()` Latitude und Longitude zu meinem Server. Ich habe einen kleines Dummy-Programm auf AppHabour in ASP.NET-MVC3 gebaut, das die Daten mittels GET über eine URL sendet.

Natürlich braucht man dafür die Interneterlaubnis (permission), die ich oben schon beschrieben habe. Der Code sieht folgendermaßen aus:

<script src="https://gist.github.com/2864460.js"> </script>

Und das wars!

Das vollständig lauffähige Projekt mit dem kompletten Code kannst du [hier downloaden][4].

Hoffentlich kann ich bald diesen ganzen Code mit einen AsyncTask zusammenpacken, um das ganze asynchron ablaufen zu lassen.

  [1]: /Media/Default/BlogPost/blog/eclipse_mainxml_Design.JPG
  [2]: http://developer.android.com/guide/topics/location/obtaining-user-location.html
  [3]: http://developer.android.com/reference/android/location/Geocoder.html
  [4]: https://www.dropbox.com/s/5qp1rbo44sw1si9/AndroidAddressApp.zip?dl=0
