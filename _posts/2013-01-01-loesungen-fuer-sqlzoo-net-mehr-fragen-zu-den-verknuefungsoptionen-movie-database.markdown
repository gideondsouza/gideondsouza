---
layout: post
title: Lösungen für sqlzoo.net Mehr Fragen zu den Verknüfungsoptionen (Movie Database)
tags:
- sql
---

Als ich so durch das Internet wanderte auf der Suche nach sql-Übungen und -Tutorials bin ich auf die Seite [www.sqlzoo.net][1] gestoßen.

Wenn man irgendetwas über SQL wissen will, insbesondere über Verknüfungen, dann ist man hier an der richtigen Adresse.

Unten habe ich Lösungen für die Fragen des [Mehr Verknüfungen][2] Tutorials zusammengetragen. Die Fragen 1-6 sind schlicht und einfach. Fragen 7-11 sind grundlegende Fragen zu Verknüfungen (joins) und 12-16 sind ziemlich knifflig. Letzete zu lösen war für mich ziemlich zeitraubend.

Hier sind sie, all die Lösungen für den Fall, dass Du mal gestrandet sein solltest. (Ich hab einfach alle Fragen der Vollständigkeit halber aufgelisted)


### Problem 1 : Liste alle Filme auf, für welche yr ist 1962 [Show id, title]
Diese Lösung ist ziemlich straightforward.

<script src="https://gist.github.com/3551780.js"> </script>

### Problem 2 : Gib das Jahr für 'Citizen Kane' aus.
Ebenfalls simpel:

<script src="https://gist.github.com/3551783.js"> </script>

### Problem 3 : Liste alle Star Trek Filme auf, einschließlich der ID, dem Titel und Jahr. (Alle dieser Filme beinhalten die Worte Star Treck in ihrem Titel.)

<script src="https://gist.github.com/3551454.js"> </script>

### Problem 4 : Wie lauten die Titel der Filme mit der id 11768, 11955, 21191?

<script src="https://gist.github.com/3551463.js"> </script>

### Problem 5 : Welche Id-Nummer hat der Schauspieler 'Glenn Close'?

<script src="https://gist.github.com/3551476.js"> </script>

### Problem 6 : Was ist die id des Films 'Casablanca'?

<script src="https://gist.github.com/3551479.js"> </script>

------
## Hier kommen die echte join-Fragen:

### Problem 7 : Liefe die Liste des Casts von 'Casablanca'. Benutze dafür den id-Wert, den Du bereits bei der vorhergehenden Frage ermittelt hast.

<script src="https://gist.github.com/3551492.js"> </script>

### Problem 8 : Liefe die Liste des Casts von 'Alien'

<script src="https://gist.github.com/3551529.js"> </script>

### Problem 9 : Liste die Filme auf, in denen 'Harrison Ford' aufgetreten ist

<script src="https://gist.github.com/3551537.js"> </script>

### Problem 10 : Liste die Filme auf, in denen 'Harrison Ford' aufgetreten ist - aber keine Star-Rolle besetzt. [Anmerkung: Das ord field von casting gibt die Position des Schauspielers wieder. Wenn ord=1, dann besetzt dieser Schauspieler die Hauptrolle]

<script src="https://gist.github.com/3551544.js"> </script>

### Problem 11: Liste die Filme zusammen mit der Hauptrolle für alle 1962 Filme auf.

<script src="https://gist.github.com/3551556.js"> </script>
--------

## Schwierige Fragen.
### Diese Fragen sind etwas schwieriger. Nimm dir etwas Zeit um sie zu lösen bevor du dir Lösungen anschaust.

### Problem 12 : Welches waren die ereignisreichsten Jahre für 'John Travolta'. Zeige die Anzahl der Filme an, die er jedes Jahr gemacht hat.

<script src="https://gist.github.com/3551570.js"> </script>

### Problem 13 : Liste die Film Titel und Hauptrollen für alle 'Julie Andrews' Filme auf.

<script src="https://gist.github.com/3551578.js"> </script>

### Problem 14 : Gib eine Liste der Schauspieler aus, welche mindestens 30 Hauptrollen innehatten. (Ja, das Resultat-set, dass damit generiert wird, ist ein leeres set)

<script src="https://gist.github.com/3551585.js"> </script>

### Problem 15 : Liste die 1978 Filme nach Größe des Casts auf.

<script src="https://gist.github.com/3551594.js"> </script>

### Problem 16 : Liste alle Personen auf, welche mit 'Art Garfunkel' zusammengearbeitet haben.

<script src="https://gist.github.com/3551605.js"> </script>

Das wars! Ich hoffe, es hat geholfen!


  [1]: http://www.sqlzoo.net
  [2]: http://sqlzoo.net/wiki/More_JOIN_operations
