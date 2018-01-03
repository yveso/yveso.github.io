---
layout: post
title: 'Haskell, wir könnten gute Freunde werden.'
---

Es ist Winter, die Tage sind kurz, das Wetter ist ungemütlich. Es ist die Zeit, in welcher man sich einen schönen Tee kocht und sich Dingen zuwenden kann, denen man sich schon immer mal zuwenden wollte.
In meinem Fall ist das (unter anderem) [Haskell](https://www.haskell.org/), als Primärquelle dient mir das Buch "Learn You a Haskell for Great Good!" von Miran Lipovača (online [hier](http://learnyouahaskell.com/chapters) frei lesbar).
<!--more-->

Was Haskell genau ist, haben andere schon an vielen Stellen geschrieben, so dass ich das nicht wiederholen will. Warum der funktionale Ansatz toll und nützlich ist, zeigt dieser (heute noch sehenswerte) [Talk](https://channel9.msdn.com/Blogs/pdc2008/TL11) auf amüsante Art und Weise.

Ich möchte lieber meine Faszination für diese Sprache ausdrücken, auch wenn ich noch relativ am Beginn meiner Reise stehe.
Hierzu schauen wir uns eine eigene Implementierung der "üblichen" `filter` Funktion an, welche viele Konzepte in sich vereint. Diese nimmt ein Prädikat (also eine Funktion welche für ein Element einen boolschen Wert zurückgibt) und eine Liste entgegen und gibt die mittels dieses Prädikats gefilterte Liste zurück (diese Funktion existiert auch in der Standard Bibliothek, man *muss* sie nicht selbst schreiben, aber man *kann*). Das Musterbeispiel ist schamlos aus dieser [Vorlesung](https://www.youtube.com/watch?v=lDqrgkDJVXo) ~~geklaut~~ übernommen.

```haskell
filter' :: (a -> Bool) -> [a] -> [a]
filter' _ [] = []
filter' p (x:xs)
    | p x = x : filter' p xs
    | otherwise = filter' p xs
```

Das Hochkomma ist in Haskell ein erlaubtes Zeichen in Namen, es wird benutzt um eigene und/oder leicht abgewandelte Versionen von Funktionen zu kennzeichnen.

## <a name="typesig"></a>Type Signatures

Die Zeile `filter' :: (a -> Bool) -> [a] -> [a]` ist die Signatur der Funktion. Nach dem `::` sehen wir die Parameter und die Ausgabe der Funktion. Für den Moment können wir das so lesen, dass das letzte Argument die Ausgabe und alle anderen davor die Eingangsparameter sind (das ist nicht 100% korrekt, dazu später mehr). Die Funktion nimmt also mit `(a -> Bool)` eine Funktion, welche ein Element vom Typ a annimmt und ein Bool ausgibt, und mit `[a]` eine Liste von Elementen des Typs a entgegen und gibt dann wieder mit `[a]` eine Liste vom Typ a zurück. `[a]` bedeutet hier lediglich *eine* Liste vom Typ a, die beiden `[a]` müssen nicht die gleiche Liste sein. `a` wird nicht näher definiert oder eingeschränkt, somit kann `a` jedem Typen entsprechen.

Somit sehen wir schon anhand der Signatur, dass Haskell über

* Polymorphismen
* ein Type System
* Higher Order Functions

verfügt. Type Signatures zu definieren ist optional, Haskell verfügt über Type Inference.

## Pattern Matching

Haskell verfügt über Pattern Matching. Hierzu werden einfach hintereinander verschiedene Szenarien angegeben, welche in dieser Reihenfolge ausgewertet werden. In Zeile zwei definieren wir den Fall, dass `filter'` mit der leeren Liste aufgerufen wird. Da diese nicht weiter gefiltert werden kann, soll wieder eine leere Liste zurückgegeben werden. Das Prädikat ist dabei unerheblich, daher wählen wir hierfür den Namen `_` (ähnlich wie in anderen Programmiersprachen).
Ab Zeile drei beschreiben wir den Fall, wenn die Funktion mit dem Prädikat `p` und einer Liste, welche `x:xs` genannt wird (siehe nächster Punkt) aufgerufen wird.

## Listen, `:` und Destructuring

Listen können in Haskell in der Form `[1,2,3]` angegeben werden. Mit dem "Operator" `:` (Hint: es ist eine Funktion) kann ein Element an die erste Stelle einer Liste eingefügt werden. `5 : [1,2]` führt zu der neuen Liste `[5,1,2]`.

Der Clou dabei ist, dass `:` nicht einfach ein Operator (oder in einer Objektorientierten Sprache eine Methode der Klasse List) ist. Listen in Haskell werden intern sukzessive durch `:` aufgebaut. `[]` ist die leere Liste, eine Liste mit einem Element `[1]` entspricht intern `1 : []`, die Liste `[2,1]` entspricht `2 : 1 : []`, usw. Die Schreibweise als Liste ist lediglich syntaktischer Zucker.

In der dritten Zeile der Funktion sehen wir den Ausdruck `(x:xs)`. Dies entspricht also einer Liste. `x` ist ein Element und xs ist im Minimalfall die leere Liste (oder eben eine nicht leere Liste). Da `x` ein Element ist (kein Null-Wert o.ä.), entspricht `x:xs` also mindestens der Liste `[x]` oder einer Liste mit mehr als einem Element und `x` an erster Stelle. `x` ist der Head und `xs` der Tail der Liste. Die Schreibweise `x:xs` scheint aber idiomatisch zu sein (lies x ist Singular, x**s** ist Plural).

Der Vorteil an der Angabe in `:` Schreibweise ist, dass die Liste nun bereits "destructured" ist und wir somit `x` bzw. `xs` direkt weiterverwenden können. Man hätte auch schlicht bspw. `list` als Parameternamen für die Liste angeben können und in Folge die Funktionen `head` und `tail` auf `list` anwenden können. Aber das wäre deutlich uncooler...

## Guards

Wenn innerhalb des gleichen Patterns unterschiedliche Wege gegangen werden sollen, kann man Guards verwenden, zu sehen in den Zeilen vier und fünf. Zwischen Pipe und Gleichheitszeichen werden Wahrheitsausdrücke, nach dem Gleichheitszeichen das Auszuführende angegeben. Das finale "else" wird mit `otherwise` deklariert.

Es wird also das Prädikat `p` auf das Element `x` angewandt. Wenn dieser Aufruf `True` ergibt, wird `x` vor die Liste, welche `filter'` angewandt auf `xs` (den Rest der Liste) erzeugt, gehängt (Man kann erahnen, um was es im nächsten Punkt gehen wird). Ansonsten wird einfach nur `filter'` mit `xs` aufgerufen.

## Rekursion

Ein solcher Block muss folgendes Zitat beinhalten:

> Um Rekursion zu verstehen, musst du Rekursion verstehen.

Rekursion ist nicht das absolut beliebteste Werkzeug. In Haskell ist sie aber, meiner Meinung nach, eine Spur klarer. In handelsüblichen prozeduralen Programmiersprachen wird die Abbruchbedingung oft in einen If Block zu Beginn einer Funktion gepackt, gefolgt vom eigentlichen rekursiven Aufruf. Mit Pattern Matching (oder Guards) in Haskell lassen sich Abbruchbedingung und rekursiver Aufruf auf dem gleichen Nesting Level definieren. Das macht Rekusrion nicht auf einen Schlag supereinfach, aber eben ein kleines bisschen hübscher und ist näher am mathematischen Vorbild. Vergleichen wir eine mathematische Definition der Fakultät mit Implementierungen in Haskell und Python (ich mag dich trotzdem), wird dies deutlich.

### Mathematik

$$
\begin{equation}
   n! =
   \begin{cases}
     1 & \text{wenn } n = 0 \\
     n*(n-1)! & \text{sonst}
   \end{cases}
\end{equation}
$$

### Haskell

```haskell
factorial 0 = 1
factorial n = n * factorial (n-1)
```

### Python

```python
def factorial(n):
    if n == 0:
        return 1

    return n * factorial(n-1)
```

## Partial application

Wie unter [Type Signatures](#typesig) beschrieben, können wir uns unsere `filter'` Funktion so vorstellen, dass sie zwei Parameter (die Funktion zum Filtern und eine Liste) entgegennimmt. Das ist nicht falsch, aber auch nicht ganz richtig. Es ist so, dass Funktionen in Haskell immer nur einen Parameter entgegen nehmen (und ich mache jetzt einen Absatz, damit der Leser das verdauen kann).

Aber die `filter'` Funktion nimmt doch klar zwei Parameter entgegen?

Stimmt, Funktionen in Haskell haben einen Parameter, Funktionen mit mehreren Parametern geben "Zwischenfunktionen" zurück. In unserem Beispiel ist es so: `filter'` nimmt einen Parameter vom Typ `(a -> Bool)` an und gibt dann eine Funktion zurück, welche einen Parameter vom Typ `[a]` annimmt. Diese Funktion gibt dann einen Wert vom Typ `[a]` zurück. Dadurch erklärt sich auch die, anfangs nicht zwingend intuitive, Syntax der Signatur `(a -> Bool) -> [a] -> [a]`.

Das ist ja schön und gut, aber was nützt das?

Der Witz ist, dass wir diese "Zwischenfunktionen" nutzen können, in dem wir eine solche Funktion mit "zu wenigen" Parametern aufrufen (Wir führen sie nur teilweise aus). Wenn wir unsere Funktion nur mit der Funktion `even` (gibt zurück ob eine Zahl gerade ist), aber keiner Liste aurufen (und dem ganzen einem Namen geben), erhalten wir eine Funktion mit der wir direkt aus Listen die geraden Zahlen filtern können. Das Beispiel mag trivial sein, but you may get the point.

```haskell
ghci> let filterEven = filter' even
ghci> filterEven [1..20]
[2,4,6,8,10,12,14,16,18,20]
ghci> filterEven [100..110]
[100,102,104,106,108,110]
ghci> filterEven [1,3..49]
[]
```

Exkurs: In der ersten Zeile definieren wir die neue Funktion ohne explizit einen Parameter anzugeben. Das sieht komisch aus, ist in diesem Fall aber auch nicht nötig, man recherchiere [Pointfree Style](https://wiki.haskell.org/Pointfree).

Da alles eine Funktion ist, kann man damit Spaß haben. `<` ist eine Funktion, welche zwei Parameter entgegen nimmt und vergleicht. `(3<4)` ist `True`. `(<5)` ist dagegen eine Funktion, welche einen Parameter entgegen nimmt und diesen mit 5 vergleicht. Wir können diese Funktion direkt verwenden. Wir benötigen keine explizite neue Funktion oder einen Lambda Ausdruck. Das würde zwar auch funktionieren, ist aber nicht nötig.

```haskell
ghci> filter' (<5) [1..10]
[1,2,3,4]
ghci> let isLessFive = (<5)
ghci> filter' isLessFive [1..10]
[1,2,3,4]
ghci> filter' (\x -> x<5) [1..10]
[1,2,3,4]
```

Auch das sieht ungewohnt und komisch aus, aber sobald man sich daran gewöhnt (oder abgefunden) hat, lässt sich sehr präziser Code fabrizieren.
