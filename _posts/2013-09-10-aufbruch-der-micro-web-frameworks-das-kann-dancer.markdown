---
layout: post
title:  Aufbruch der micro web frameworks: Das kann dancer
date:   2013-09-10
tags:
- web-dev
- dancer
---

Micro-frameworks scheinen richtig _**in**_ zu sein, im Moment, da wären:

* [Sinatra](http://www.sinatrarb.com/) für Ruby (Das ist der Großvater, der alle anderen inspiriert hat)
* [Dancer](http://www.perldancer.org/) für Perl
* [Flask](http://flask.pocoo.org/) für Python
* [Nancy](http://nancyfx.org/) für .NET
* [Scotty](http://www.ittc.ku.edu/csdl/fpg/software/scotty.html) für Haskell

Ich habe Dancer ziemlich häufig benutzt und kürzlich http://www.perlmonksflair.com damit gebaut.

So sieht eine einfache Dancer-App aus:

Speichere das folgende in my_app.pl

<script src="https://gist.github.com/gideondsouza/6508444.js"></script>

Dann kommt folgendes in die command line:

    $ perl my_app.pl &
    ...
    $ curl http://localhost:3000/
    Hello world!

Wenn du schon etwas web-Entwicklung-Erfahrung hast, kriegst du das vermutlich hin und verstehst was vor sich geht. Die line `get '/' => sub {}` registriert die url : / with mit einer subroutine, oder, etwas präzisier gesprochen, einer coderef (eine Referenz auf eine subroutine)

Das heißt die Homepage (z.B. www.example.com/) wird "Hello world" im Browser anzeigen.  (In perl wird das letzte statement in sub der Rückgabewert sein)

Wenden wir uns etwas komplizierteren zu. Wird ein Webservice benötigt, kann einfach dieses plugin benutzt werden [Dancer::Plugin::REST](https://metacpan.org/module/Dancer::Plugin::REST). Diese Probe ist direkt aus der POD für das Plugin kopiert worden :P

<script src="https://gist.github.com/gideondsouza/6508454.js"></script>

Anzumerken ist, dass falls du persönich eine route hinzufügen musst, die json zurückgibt, du jederzeit die [to_json](https://metacpan.org/module/Dancer#to_json-structure-options) -Methode aus einer sub nutzen kannst.

Benötigst du eine github-Authentifizierung in deiner Anwendung? Benutze einfach dieses Plugin [Dancer::Plugin::Auth::Github](https://metacpan.org/module/Dancer::Plugin::Auth::Github), ja, das habe ich geschrieben! :

<script src="https://gist.github.com/gideondsouza/6508472.js"></script>

Ja, es gibt auch ein Plugin um eine Authentifizierung für Twitter durchzuführen, [und noch mehr Plugins um anderen coolen Kram zu machen](https://metacpan.org/search?q=Dancer%3A%3APlugin) .

Also, worauf wartest du? Mach schon und tranz dir deinen Weg hinein in die web-Anwendungswunderwelten.
