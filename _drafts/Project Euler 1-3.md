---
layout: post
title: Project Euler&#58; Probleme 1-3
---

[Project Euler](https://projecteuler.net/) ist eine Website, welche eine Sammlung von Programmieraufgaben bereitstellt. Benannt ist diese Seite nach Leonhard Euler, der wie Carl Friedrich Gauß, nicht nur ein Faible für fesche Kopfbedeckungen hatte, sondern auch zu den größten der Mathematik zählt. Wer sich an die e-Funktionen aus der Schule erinnert, die heißen so, weil **e** für die **E**ulersche Zahl steht. By the way, der Begriff *Funktion* ist auch von ihm. Somit können wir auch aus der Programmierperspektive den Hut vor ihm ziehen.

![Leonhard Euler]({{ site.url }}/assets/images/blog/2018/Leonhard_Euler.jpg)

{:.image-caption}
*Er kann zufrieden mit sich sein... Portrait von Jakob Emanuel Handmann [Public domain], via Wikimedia Commons*

Was Project Euler von ähnlichen Seiten abhebt, ist, wer hätte es bei diesem Namen gedacht, dass die Aufgaben (welche Probleme genannt werden) sehr mathematisch geprägt sind. Das ist zugleich Vor-, als auch Nachteil. Da die meisten Probleme so designt sind, dass Brute Force kein gangbarer Weg ist, muss man bei den gehobeneren Problemen den "Kniff" kennen. Die Recherche danach kann sehr erfüllend sein, aber wenn man einfach nur ein wenig Code fabrizieren will, ist man auf anderen Seiten eventuell besser aufgehoben.

Nach und nach möchte ich in diesem Blog verschiedene Probleme lösen und kommentieren. Ich liefere hierbei den kompletten Code, möchte aber die jeweilige Lösung nicht explizit nennen, um den Cheatern es nicht noch einfacher zu machen. XXXXXXXXXXXXXXXXXXXXXXXXX
<!--more-->

## Problem 1

> If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.
> Find the sum of all the multiples of 3 or 5 below 1000.
>
> <cite>[https://projecteuler.net/problem=1](https://projecteuler.net/problem=1)</cite>

Das klingt zunächst nicht über die Maßen schwierig und erinnert ein wenig an Fizz Buzz. Die Crux ist die Gleiche, man muss den Modulo Operator kennen. Wenn wir diesen kennen, können wir die natürlichen Zahlen bis (exklusive) 1000 durchlaufen, für jede Zahl überprüfen ob sie ein Vielfaches von 3 oder 5 ist und alle diese Zahlen addieren. Eine, sehr prozedurale Lösung könnte also wie folgt aussehen:

```python
def def solve_1_procedural():
    sum = 0
    for x in range(1_000):
        if x % 3 == 0 or x % 5 == 0:
            sum = sum + x
    return sum
```

Das funktioniert und liefert die korrekte Lösung. Aber wirklich glücklich macht es uns nicht. Überlegen wir, wie eine deklarative, funktionale Lösung aussehen könnte. Wir möchten eine Teilmenge bilden und diese dann summieren, das klingt nach *Map, Filter and Reduce*. Da wir die Zahlen an sich nicht verändern, entfällt sogar der Map Schritt. Auf zum Batmobil!

```python
from functools import reduce

def solve_1_map_filter_reduce():
    return reduce(
        lambda x, y: x + y,
        filter(
            lambda x: x % 3 == 0 or x % 5 == 0,
            range(1000)
        )
    )
```

Das liefert die gleiche Lösung. Aber sind wir jetzt glücklicher? Eher nicht, eigentlich ist alles sogar schlimmer. Aber behalten wir die Grundidee und schauen, welche Wege es noch gibt. Python verfügt über *List Comprehensions* und hat auch eine sum Funktion...

```python
def solve_list_comprehension():
    return sum([x for x in range(1000) if x % 3 == 0 or x % 5 == 0])
```

List Comprehensions sind schön, aber brauchen wir für unser Ergebnis wirklich eine Liste als solche? Oder reichen uns nicht auch die einzelnen Werte zur Bestimmung unserer Summe? Python hätte nämlich auch **Generator Expressions**, aber das ist Fleißarbeit.

```python
def solve_generator_expressions():
    return sum(x for x in range(1000) if x % 3 == 0 or x % 5 == 0)
```

In Programmiersprachen, welche über ein Pipeline Konzpet verfügen, lassen sich ebenfalls XXXXXXXXXXXXX

```csharp
public int Solve()
{
    return
        Enumerable.Range(1, 999)
        .Where(x => x % 3 == 0 || x % 5 == 0)
        .Sum();
}
```

```fsharp
let solve =
    [1..999]
    |> Seq.filter (fun x -> x % 3 = 0 || x % 5 = 0)
    |> Seq.sum
```
