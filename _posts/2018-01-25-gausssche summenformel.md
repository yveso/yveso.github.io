---
layout: post
title: Die Gaußsche Summenformel
---

Meine Zeiten als Student der Mathematik liegen nun schon etwas länger zurück. Vieles des damals Gelernten müsste ich heute nachschlagen. Doch eine Sache hat sich in mein Hirn eingebrannt: der **kleine Gauß** (a.k.a. die Gaußsche Summenformel). Dabei handelt es sich um eine kleine, feine Formel, mit welcher man sehr einfach die Summe aller natürlichen Zahlen (das sind die positiven, ganzen Zahlen, also 1, 2, 3, usw...) von `1` bis zu einer Zahl `n` bestimmen kann.

Der Legende nach wurde diese Formel von einem kleinen Jungen namens Carl Friedrich Gauß (wieder-) entdeckt. Aus diesem kleinen Jungen sollte ein paar Jahre später der Godfather der Mathematik werden, aber wer konnte das zu diesem Zeitpunkt schon ahnen. Angeblich stellte der Lehrer des kleinen Carl Friedrich der Klasse die Aufgabe die Zahlen von 1 bis 100 zusammenzuzählen, um Zeit für andere Dinge zu haben. Doch ein Schüler wusste prompt die Antwort... (Details finden sich bei [Wikipedia](https://de.wikipedia.org/wiki/Gau%C3%9Fsche_Summenformel#Herkunft_der_Bezeichnung))

Wer mit dem Namen Carl Friedrich Gauß nichts anfangen kann, der kennt wahrscheinlich trotzdem sein Gesicht, da es den letzten Zehn Mark Schein zierte. Somit ergibt sich automatisch eine Assoziation zu Taschengeld. Man muss sich daher nicht weiter mit seinem Werk beschäftigen, um zu erkennen, dass er ein flyer Dude war (die Beschäftigung mit seinem Werk lohnt sich aber trotzdem).

![Zehn Mark Schein]({{ site.url }}/assets/images/blog/2018/banknote_10_deutsche_mark.jpg)

{:.image-caption}
*C.F.G. rockt den Beanie! Bildquelle: Deutsche Bundesbank, Frankfurt am Main*

Die Formel an sich ist nicht übermäßig kompliziert oder komplex. Aber sie ist umgeben von einer wunderbaren Eleganz, so dass sie in die Kategorie "genial einfach, einfach genial" fällt und ich hier das eine oder andere Wort über diese Formel verlieren möchte.
<!--more-->

## Eine gerade Zahl als Grenze

Ich möchte nicht mit der Formel selbst beginnen, versetzen wir uns lieber in die Lage des kleinen Carl Friedrich und suchen sie selbst. Um ein tatsächliches Zusammenzählen im Kopf auszuschließen, wollen wir die Summe der natürlichen Zahlen von Eins bis Eintausend ermitteln (falls du das wirklich im Kopf addieren willst, dann nun ja). Unsere Aufgabe lautet also wie folgt:

```
1 + 2 + 3 + 4 + ... + 997 + 998 + 999 + 1000
```

Der Trick zur Entdeckung unserer Formel ist, dass wir diesen Strang in der Mitte teilen. Wir betrachten die Summe von `1` bis `500` und die Summe von `501` bis `1000`. Da die Reihenfolge bei der Addition keine Rolle spielt (`1 + 2 = 2 + 1`), kehren wir diese bei der zweiten Summe um.

```
1 + 2 + 3 + ... + 498 + 499 + 500 +
1000 + 999 + 998 + ... + 503 + 502 + 501
```

Um den dadurch entstanden Effekt visuell zu verstärken, fügen wir noch ein paar Leerzeichen ein.

```
   1 +   2 +   3 + ... + 498 + 499 + 500 +
1000 + 999 + 998 + ... + 503 + 502 + 501
```

Vertikal haben sich Paare gebildet und alle Paare haben eine Gemeinsamkeit: Ihre Summe ist immer `1001`. Insgesamt haben wir `500` dieser Paare. Somit können wir unsere Aufgabe lösen in dem wir `500 * 1001` berechnen. Das hört sich schwierig an, aber dafür müssen wir nur `5 * 1001` berechnen (Tipp: es sind `5005`) und dann an diese Zahl zwei Nullen hängen. Unsere Lösung beträgt also `500500`. Anstatt 999 Additionen durchzuführen, hat uns etwas Kreativität und eine einzelne Multiplikation gereicht. Toll!

Wir sind aber auf der Suche nach einer allgemeinen Formel, daher betrachten wir die Zahlen aus unserer Multiplikation.

Unsere gegebene Grenze für die Summe war `1000`. Der (Achtung Fremdwort!) Multiplikator unser Lösung ist `500`. Das scheint gerade die Hälfte von `1000` zu sein. Stellen wir uns vor, wir hätten die Summe bis `100` gebildet, dann hätten wir `50` Paare (`1 + 100` bis `50 + 51`), somit erhärtet sich der Verdacht, dass es sich um die Hälfte handelt. Hätten wir ein allgemeines `n` als Grenze (und `n` ist eine gerade Zahl), dann wäre der Multiplikator `n / 2`.

Der (Noch ein Fremdwort!) Multiplikant unserer Rechnung ist `1001`, bei `100` als Grenze wäre er `101`. Also immer die Grenze plus Eins. Für ein allgemeines `n` wäre es also `n + 1`.

Wechseln wir in die mathematische Schreibweise, weil sie uns unglaublich intelligent wirken lässt. Das Summenzeichen darin sieht kompliziert aus, aber eigentlich sagt es nur: "Wenn `k` (erstes `k` in der Formel) nacheinander den Zahlen von `1` bis `n` entspricht, zähle für alle diese Zahlen `k` (zweites `k` in der Formel, also die Zahl wie sie ist) zusammen.

$$
\begin{equation}
   \sum_{k=1}^n k = \frac{n}{2} * (n+1)
\end{equation}
$$

Das schreiben wir noch als gemeinsamen Bruch und erhalten unsere Formel für die Summe aller natürlichen Zahlen von `1` bis zu einem geraden `n`:

$$
\begin{equation}
   \sum_{k=1}^n k = \frac{n * (n+1)}{2}
\end{equation}
$$

## Eine ungerade Zahl als Grenze

Aber wie können wir die Summe bis zu einer ungeraden Zahl bestimmen? Wir können dann die eigentlichen Additionen nicht in zwei gleich lange Stränge teilen, weil wir eine ungerade Anzahl an Zahlen haben. Das ist schlecht, aber wir können die Additionen bis zur letzten Zahl vor unserer Grenze teilen wie bislang und die Grenze selbst als eigene, dritte Gruppe betrachten (dieses mal formatieren wir gleich):

```
   1 +   2 +   3 + ... + 498 + 499 + 500 +
1000 + 999 + 998 + ... + 503 + 502 + 501
+
1001
```

Wir haben wieder unsere `500` Paare, die jeweils `1001` ergeben und wir haben noch eine Zahl mehr, die aber auch `1001` ist. Wir haben also `501` mal die `1001` als Lösung.

Schauen wir, ob wir das verallgemeinert bekommen. Beginnen wir dieses Mal mit dem Multiplikant (ist einfacher). Bei einer Grenze von `1001` ist er `1001`, es ist also die Grenze selbst. Für die Grenze `n` ist es somit `n`.

Für den Multiplikator müssen wir einen Weg von der Grenze `1001` zu `501` (oder von `101` zu `51`) finden. Ein Weg hierfür wäre, wenn wir die Grenze um Eins erhöhen und dann die Hälfte davon nehmen (`1001 + 1 = 1002`, `1002 / 2 = 501`). Dann ergibt sich für ein allgemeines `n` der Multiplikator `(n + 1) / 2`. Wir wollen wieder intelligent wirken und wechseln die Schreibweise.

$$
\begin{equation}
   \sum_{k=1}^n k = \frac{n+1}{2} * n
\end{equation}
$$

Das können wir wieder in einem Bruch schreiben.

$$
\begin{equation}
   \sum_{k=1}^n k = \frac{(n+1) * n}{2}
\end{equation}
$$

Und da auch bei der Multiplikation die Reihenfolge keine Rolle spielt, können wir diese im Zähler des Bruchs umdrehen.

$$
\begin{equation}
   \sum_{k=1}^n k = \frac{n * (n+1)}{2}
\end{equation}
$$

Heureka! Das ist ja die gleiche Formel wie bei der geraden Grenze. Wie schön!

## Aber Teilen kann gefährlich sein!

Die natürlichen Zahlen sind in der Addition abgeschlossen. Das heißt, wenn wir natürliche Zahlen addieren, erhalten wir immer eine natürliche Zahl als Ergebnis. `11 + 37 = 48`, `48` ist wieder eine natürliche Zahl. 5&frasl;9 ist keine natürliche Zahl, es gibt keine natürlichen Zahlen deren Summe 5&frasl;9 ist. Falls du doch welche findest, melde dich, ich gebe dir ein Getränk deiner Wahl aus.

In unserer Formel teilen wir durch `2`, bei dieser Division erhalten wir aber nur eine natürliche Zahl, wenn `n * (n + 1)` gerade ist, bei einer ungeraden Zahl erhielten wir einen Bruch (Streber sagen rationale Zahl) als Ergebnis.

Oben auf unserem Bruch (Zähler für die Streber) haben wir eine Multiplikation `n * (n + 1)`. Das Schöne an einer Multiplikation ist, dass sobald Multiplikant oder (aber auch und) Multiplikator gerade sind, dass Ergebnis auch gerade ist (Wie heißt es so schön, der Beweis hierfür sei dem Leser als Übung überlassen. Finde eine natürliche Zahl `x`, so dass bspw. `4 * x` oder `32 * x` ungerade wird, du wirst sehr lange suchen).

Beginnen wir also mit dem Multiplikator `n`, der kann gerade oder ungerade sein. Wenn `n` gerade ist, dann ist alles gut. Wenn `n` allerdings ungerade ist, dann muss `n + 1` gerade sein, damit wir teilen können. Guess what, `n + 1` ist der Nachfolger von `n`, der Nachfolger einer ungeraden Zahl ist immer gerade. Yay!

Somit ist unsere Angst vor dem Teilen unbegründet, aber gut dass wir darüber gesprochen haben.

## Aber gilt die Formel wirklich für alle natürlichen Zahlen?

Unsere Herleitung der Formel für eine gerade Zahl als Grenze ist schlüssig. Die für eine ungerade Grenze ist es auch. Da eine natürliche Zahl entweder gerade oder ungerade ist, sind wir eigentlich gut gerüstet. Man kann uns eine beliebige Zahl nennen und wir können unsere Formel anwenden. Man wird uns keine natürliche Zahl nennen können, bei welcher unsere Formel nicht funktioniert. Alles bestens, eigentlich...

Leider sind die Damen und Herren Mathematiker da etwas penibler. Die hätten da lieber erst einen formalen Beweis dafür (und das obwohl sie kein Beispiel finden könnten was uns wiederlegt, was können sie stur sein, sie sollten mal Karl Popper lesen...).

Um eine Aussage der Art "Für alle natürlichen Zahlen gilt" formal zu beweisen, gibt uns die Mathematik ein Werkzeug in die Hand, bei dem die bloße Erwähnung des Namens bei vielen Angstschweiß und schreckliche Erinnerungen hervorruft, die **vollständige Induktion**.

Ein Beweis mittels vollständiger Induktion besteht aus drei Teilen:

1. Induktionsanfang
2. Induktionsannahme
3. Induktionsschluss

Im Induktionsanfang wenden wir unsere Formel einfach praktisch an. Wir setzen hierfür die kleinste Zahl ein, für welche die Formel gültig sein soll. In unserem Fall soll die Formel für alle natürlichen Zahlen gelten, also werden wir die Formel für `1` überprüfen. Dieser Schritt ist eigentlich für so gut wie jede Formel relativ einfach.

Die Induktionsannahme ist der mit Abstand beste Teil. Er besteht eigentlich nur darin, dass wir die Annahme formulieren, dass die Formel für jede Zahl `n` korrekt ist. Es ist tatsächlich nur diese Aussage, da behaupte noch einmal jemand, dass die Mathematik immer kompliziert wäre.

Wenn diese Beweismethodik allerdings derart unbeliebt ist, der erste von drei Teilen recht einfach und der zweite Teil trivial ist, dann muss die Sache irgendwann noch einen Haken haben. Stimmt, im Induktionsschluss müssen wir zeigen, dass wenn die Formel für ein unbestimmtes `n` gültig ist (das ist unsere Annahme), sie dann auch für `n + 1` gültig ist. Dieser Teil ist also ein kleines bisschen abstrakter.

Was bringt uns das? Wenn es uns gelingt diesen Schluss zu beweisen, dann wüssten wir, dass wenn die Formel für `5` gültig *wäre*, dass sie dann auch für `6` gültig *wäre*. Wenn sie für `93` gültig *wäre*, dann auch für `94`. Wenn sie (letztes Beispiel, versprochen) für `1336` gültig *wäre*, dann auch für `1337`. Wir wissen aber nicht, ob sie für `5`, `93` oder `1336` gültig *ist*.

Damit sich der Kreis schließt, müssen wir zurück zum Anfang, zum Induktionsanfang. Für `1` haben wir die Gültigkeit explizit bewiesen. Wenn wir den Induktionsschluss auf diesen Fakt anwenden, dann wissen wir sicher, dass die Formel auch für `2` gültig *ist*. Wir können den Induktionsschluss darauf anwenden und wissen, dass die Formel für `3` gültig *ist*. Und so weiter und so fort, bis in alle Ewigkeit. Dieser Beweis überzeugt selbst die Mathematiker. Also packen wir es an:

Bevor wir wirklich loslegen, geben wir unserer Formel noch den Namen `A(n)` (A für Aussage, in Abhängigkeit von n). Damit können wir leichter ausdrücken was wir tun.

$$
\begin{equation}
   A(n) := \sum_{k=1}^n k = \frac{n * (n+1)}{2}
\end{equation}
$$

Wir starten mit dem Induktionsanfang, zunächst berechnen wir die Summe aller natürlichen Zahlen von `1` bis `1`, das müsste (wenn wir uns nicht komplett verrechnet haben) ebenfalls `1` sein.

$$
\begin{equation}
   Induktionsanfang~A(1): \sum_{k=1}^1 k = 1
\end{equation}
$$

Nun setzen wir `1` in den rechte Seite unserer Formel ein und hoffen, dass da auch `1` rauskommt.

$$
\begin{equation}
   \frac{1 * (1+1)}{2} = \frac{1 * (2)}{2} = \frac{2}{2} = 1
\end{equation}
$$

Hervorragend. Damit ist `A(1)` bewiesen, widmen wir uns der Induktionsannahme.

$$
\begin{equation}
   Induktionsannahme: A(n)~ist~wahr.
\end{equation}
$$

Und damit kommen wir schon zum Induktionsschluss.

$$
\begin{equation}
   Induktionsschluss: A(n) \Rightarrow A(n+1)
\end{equation}
$$

Wenn `A(n)` gilt, muss auch `A(n + 1)` gelten. Um dies zu zeigen, betrachten wir zunächst die Summe bis `n + 1`. Wir formen diesen Term um: In diese Summe bis `n` zu welcher wir `n + 1` explizit addieren. Da das Summenzeichen nur eine Kurzschreibweise für eine Vielzahl von Additionen ist, ist das eine erlaubte Umformung.

$$
\begin{equation}
   \sum_{k=1}^{n+1} k = \sum_{k=1}^{n} k + (n+1)
\end{equation}
$$

Der vordere Teil entspricht `A(n)`, davon haben wir ja angenommen, dass es wahr ist. Also ersetzen wir es mit dem anderen Teil unserer Formelgleichung.

$$
\begin{equation}
   = \frac{n * (n+1)}{2} + (n+1)
\end{equation}
$$

Wir bringen beide Summanden auf den Hauptnenner, so das wir die Summe als gemeinsamen Bruch schreiben können.

$$
\begin{equation}
   = \frac{n * (n+1)}{2} + \frac{2*(n+1)}{2} = \frac{n * (n+1) + 2*(n+1)}{2}
\end{equation}
$$

In dieser Summe können wir `(n + 1)` (nach vorne) ausklammern.

$$
\begin{equation}
   = \frac{(n+1) * (n+2)}{2}
\end{equation}
$$

Und eigentlich haben wir unsere Aussage jetzt schon bewiesen. Quod erat demonstrandum. Ende der Durchsage.

$$
\begin{equation}
   \blacksquare
\end{equation}
$$

Ganz ehrlich: Ich mochte und mag es noch heute auch nicht, wenn Texte abrupt enden, weil der Autor der Meinung ist, dass alles Folgende trivial wäre. Also, wir haben eine Verkettung von gleichen Ausdrücken, somit sind der erste und der letzte Ausdruck dieser Kette auch gleich und wir können schreiben:

$$
\begin{equation}
   \sum_{k=1}^{n+1} k = \frac{(n+1) * (n+2)}{2}
\end{equation}
$$

Das `n + 2` können wir umschreiben in dem wir erst `n + 1` bilden und dann noch einmal `1` addieren.

$$
\begin{equation}
   \sum_{k=1}^{n+1} k = \frac{(n+1) * ((n+1)+1)}{2}
\end{equation}
$$

Siehst du es schon? Wir können `(n + 1)` in dieser Formel durch `X` ersetzen.

$$
\begin{equation}
   \sum_{k=1}^{X} k = \frac{X * (X+1)}{2}
\end{equation}
$$

Wenn wir `X` jetzt in Gedanken mit `n` ersetzen, erkennen wir, dass wir die gleiche Formel erhalten haben. Also wenn die Formel für `n` gültig ist, dann ist sie es auch für `n + 1`.

## Fazit

Dieser Text wurde dann doch etwas länger als ursprünglich geplant. Aber ich war, bin und bleibe fasziniert davon, dass sich eine solche Summe, ganz gleich wie viele Zahlen addiert werden, auf je eine Addition (`n + 1`), Multiplikation (`n * (n + 1)`) und Division (`(n * (n + 1)) / 2`) herunterbrechen lässt. Vielleicht ist es mir gelungen, etwas davon auf dich, werter Leser, zu übertragen.

Auch im Kontext der Programmierung ist diese Formel spannend. Auch wenn die Anzahl der real existierende Anwendungsfälle für diese Formel eher gering mag, drei Instruktionen haben eine konstante Laufzeit (`O(1)`), eine Lösung über bspw. eine Schleife hätte eine lineare Laufzeit (`O(n)`). Auch wenn Donald Knuth mit "premature optimization is the root of all evil" durchaus recht haben mag, die dunkle Seite der Macht ist halt doch die deutlich Attraktivere. Aber mit einem sprechenden und dokumentierten Refactoring kann man die Formel schon verwenden.
