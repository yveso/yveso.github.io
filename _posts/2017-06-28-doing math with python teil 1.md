---
layout: post
title: 'Lesestunde: Doing Math with Python, Teil 1'
---

![Doing Math with Python]({{ site.url }}/assets/images/blog/2017/doing_math_with_python_cover.jpg)

Mathe macht Spaß. Python macht Spaß. Ein Buch mit dem Titel **Doing Math with Python** muss demnach eine niemals versiegende Quelle der Freude sein. Um herauszufinden ob dem so ist, werde ich dieses Buch in der soeben gestarteten, aber jetzt schon unglaublich beliebten, Reihe *Lesestunde* durcharbeiten.

Autor des Buches ist *Amit Saha*, erschienen ist es 2015 bei *No Starch Press*. Die Website beim Verlag findet sich [hier](https://www.nostarch.com/doingmathwithpython), die begleitende Website zum Buch (incl. Code) [hier](https://doingmathwithpython.github.io/).

Das Buch benutzt -glücklicherweise- Python 3 und setzt Grundkenntnisse voraus, Zitat: "the absolute basics".
<!--more-->

## Chapter 1: Working with Numbers

Das Buch beginnt mit einer Aufzählung der vorhandenen mathematischen Operatoren in Python. Wer Python nicht kennt, wird womöglich überrascht sein, dass in dieser Sprache sowohl ein Operator für Fließkomma- `5 / 3`, als auch für die ganzzahlige Division `5 // 3` existiert (In Python 2 war das Verhalten dieser Operatoren anders). Ebenso existiert ein Operator für Potenzen `5 ** 3`, dieser hat inzwischen auch den Weg in andere Sprachen gefunden.

Danach widmet sich der Autor Datentypen. Python ist zwar eine dynamische Programmiersprache, aber das heißt nicht, dass es keine Datentypen gibt. Neben den üblichen Verdächtigen `int` und `float` bietet Python frei Haus auch Klassen für komplexe Zahlen und Brüche (über das fractions module). Sehr beliebte Hausaufgaben sind somit in Python obsolet. :)

```
>>> c = 5 * 3j
>>> print(type(c))
<class 'complex'>
>>> print(c.real)
5.0
```

```
>>> from fractions import Fraction
>>> f = Fraction(1, 3)
>>> print(type(f))
<class 'fractions.Fraction'>
>>> print(f.denominator)
3
```

Das Kapitel schließt mit Erläuterungen zu typischen Builtin Funktionen wie `input()` oder `range()`, sowie ein paar Aufgaben für den Leser, auf welche ich hier nicht näher eingehen werde.

Habe ich in diesem Kapitel etwas grundlegend neues gelernt? Eher nicht, aber da sich das Buch auch an Neulinge wendet, ist das auch in Ordnung. Kapitel 2 behandelt dann Visualisierungen und verspricht auch für den etwas erfahreneren Leser interessanter zu werden.

[Notebook mit Beispielcode aus diesem Kapitel](https://github.com/yveso/notebooks/blob/master/blog/2017/Doing_math_with_python_chapter_1.ipynb)
