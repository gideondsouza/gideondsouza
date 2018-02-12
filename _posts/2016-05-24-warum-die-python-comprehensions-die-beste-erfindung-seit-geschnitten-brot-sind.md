---
layout: post
title:  Warum die Python comprehensions die beste Erfindung seit geschnitten Brot sind
tags:
- python
- functional
---

Seit ich damals angefangen habe mich in meiner Freizeit mit [Perl](http://metacpan.org/author/GIDEON) und Python zu beschäftigen, bin ich sehr überzeugt davon, was [Bjarne Stroustrup einmal hier gesagt hat](http://www.youtube.com/watch?v=NvWTnIoQZj4) : "Niemand sollte sich selbst (einen) professionell(en Coder) nennen, wenn er nur eine Sprache kennt. Fünf ist ein ganz guter Richtwert."

Als ich [Linq](http://en.wikipedia.org/wiki/Language_Integrated_Query) entdeckte, dachte ich ganz hochmütig, C# sei anderen Sprachen deutlich überlegen, denn leider kannte ich da Python noch nicht.

Nachdem ich Python comprehensions über [diesen coursera-Kurs den ich gemacht habe](https://www.coursera.org/course/matrix) kennenlernte, war ich begeistert.  Python comprehensions sind meiner Meinung nach mindestens das Beste seit es geschnitten Brot gibt.

Hier eine kleine Übersicht was man so mit Phyton comprehensions anstellen kann.

Python hat bereits eingebaute _dictionary_, _list_, _set_ und _tuple_. Im Kern ist eine comprehension eine kurz und bündige Möglichkeit eine dieser Strukturen zu evaluieren oder zu generieren.

Downloade das [neuste Python](http://python.org/download/releases/3.3.2/). Egal auf welchem Betriebssystem du gerade unterwegs bist, öffne einfach ein Eingabeaufforderungsfenster (Command Prompt window), und tippe python ein, und folge dann den Auszügen unten. Anmerkung: Macs haben Phyton bereits vorinstalliert, öffne einfach das Terminal und tippe phyton ein.


<script src="https://gist.github.com/gideondsouza/6460345.js"></script>

Für einen Ausdruck wie diesen : `[x for x in range(10)]` . gibt range(N) eine zählbare oder "loopable" (also in Schleifen bearbeitbare) Struktur zurück. In dem Teil zwischen der `[` und dem `for` kann x genutzt und so ziemlich alles mit ihm angestellt oder ein Ausdruck zuückgegeben werden.

Hier ein eher blödes Gegenbeispiel : `[5 for x in range(5)]`. Das generiert eine Liste : `[5, 5 , 5 , 5 ,5]`. Wenn du aber das hier machst : `[x*5 for x in range(5)]`, bekommst du die Vielfachen von Fünf.

Vielleicht ist klargeworden, was ich meine. Wenn du jetzt deine Liste baust, kannst du noch weitere Entscheidungen hinzufügen.

<script src="https://gist.github.com/gideondsouza/6460422.js"></script>

Jetzt kann ich den set-Datentyp vorstellen. Ein set ist in python eine unsortierte Liste **einzigartiger** (unique) Einheiten (items).  Anmerkung: Um ein leeres set zu erstellen macht man folgendes : `s = set()`.  Macht man das hier `x={}`, dann wird x ein dictionary. Hier findest du die [python docs für ein set.](http://docs.python.org/3/tutorial/datastructures.html#sets)

<script src="https://gist.github.com/gideondsouza/6460529.js"></script>

Der nächstwichstigste Datentyp ist das tuple, und die python docs über tuples findest du hier :

<script src="https://gist.github.com/gideondsouza/6460607.js"></script>

Nun wirds richtig abgefahren, wir benutzten zwei Schleifen (loops) in unserer comprehension um Permutationen und Kombinationen der Zahlen 1 bis 5 zu kreieren

<script src="https://gist.github.com/gideondsouza/6460685.js"></script>

Na, überzeugt?
