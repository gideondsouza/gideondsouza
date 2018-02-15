---
layout: post
title:  Bilder mit Ruby und Sinatra hochladen
tags:
- ruby
- web-dev
- sinatra
---

Ihr habt bestimmt inzwischen gemerkt, dass ich eine Vorliebe für [Microframeworks](http://www.gideondsouza.com/blog/the-dawn-of-the-micro-web-frameworks-introducing-dancer/) habe.

Ich hab mich letztens mal drangestetzt Ruby zu lernen. Meine Erfahrung ist, dass dicke Bücher und guides zu lesen ziemlich langweilig werden kann und oft auch nicht wirklich hilfreich ist. 80% was man mit einer Sprache anfangen kann kann man eigentlich durch das lernen der wichtigsten 20% hinkriegen. 
(In Ankehnung an das [Pareto-Prinzip](https://en.wikipedia.org/wiki/Pareto_principle))

Ich fange immer mit dem Ziel an etwas in der Programmiersprache **machen** zu können, die ich gerade lerne. Auf diese Weise lerne ich eben diese wichtigsten 20%.

Der Großteil der Entwicklung dreht sich heute fast ausnahmslos um Webdevelopement, deswegen kommt man irgendwann an den Punkt, an dem man gerne eine Web-App bauen möchte. Mikroframeworks bieten einen guten Start dafür.

Also habe ich ein bisschen mit Ruby und [Sinatra](sinatrarb.com) herumgespielt und habe mir dafür entschieden eine Art Dateimanager zu bauen, und ihn vielleicht noch in Dropbox zu integrieren, mal schauen.

**Das hier ist die erste Runde** des Plans, eine einfache, kleine Web-App zu erstellen, die Bilder in einen Ordner hochläd und dir danach das Bild nach dem Hochladen noch einmal anzeigt.

Stelle sicher, dass du Ruby hast und installiere Sinatra wie folgt:

    gem install sinatra

Danach sollten deine Dateien so aussehen (der Code steht unten):

    [gideon@gideon-fedora image_manager]$ tree
    .
    ├── img_mgr.rb
    ├── public
    └── views
        ├── form.erb
        └── show_image.erb

Ein kurzes Ablaufprokoll:

* Sinatra bietet statische Dateien aus einem Ortner namens _public_ an. Wir werden unser Bild in diesen Ordner schreiben.
* Wir benutzen erb, und ja, es gibt einfach [so viele Anzeige-Engines](http://www.sinatrarb.com/intro.html#Available%20Template%20Languages). Diese coolen kids scheinen Haml zu mögen.
* Wir haben zwei routes (1) _'/'_ und (2) _'/show_image'_ ermöglichen wie gesehen den Upload (1) _form.erb_ und der anschließenenden Anzeige des Bildes mit _show_image.erb_

Hier der dazugehörige Code :

<script src="https://gist.github.com/gideondsouza/fc7e990030b17884d79efb28b74ced2e.js"></script>

<script src="https://gist.github.com/gideondsouza/f3a55300cc1002054fdf17ddd2468e38.js"></script>

<script src="https://gist.github.com/gideondsouza/aa2396b5cd59429f4a082b05f4c8bc3f.js"></script>


Ich hoffe, dass das meiste davon selbsterklärend und hilfreich dabei ist, wenn du dich selbst ans Werk machst. Ich werde versuchen hierdraus eine Serie zu machen, in welcher ich schritttweise eine richtige kleine Web-App entwickle.
