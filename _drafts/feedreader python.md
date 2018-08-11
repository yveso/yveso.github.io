---
layout: post
title: Ein RSS Reader in Python
---

Die längst vergangenen Zeiten des Web 2.0 verhalfen einer Technologie zum Durchbruch, die sich [RSS Feed](https://de.wikipedia.org/wiki/RSS_(Web-Feed)) nennt. Ohne allzu sehr in die Details oder gar die Spezifikationen zu gehen, was ist das?

Ein RSS Feed ist (ein möglicher Anwendungsfall) eine alternative Version einer Website. Während die "normale" Version für den Menschen gedacht ist, ist der dazugehörige Feed für Maschinen oder Programme gedacht. Wenn du die Adresse dieser Website [https://yveso.github.io](https://yveso.github.io) aufrufst, wird der Browser eine Datei downloaden, ein paar Schritte Magie vollführen und dir letztendlich die Seite mit ihren Beiträgen in einem vorher definierten Design anzeigen. Wenn du dagegen den Feed dieser Seite [https://yveso.github.io/atom.xml](https://yveso.github.io/atom.xml) aufrufst, zeigt der Browser eine gänzlich unmagische Datei im XML Format dar. Diese enthält ein paar Informationen zur Seite und, deutlich spannender, auch die eigentlichen Beiträge. Manche Feeds enthalten alle Beiträge einer Seite, andere nur die neusten. Manche enthalten die Beiträge vollständig, andere nur Anrisse. Ein Feed ist (in unserem Anwendungsfall) eine Art Nachrichtenticker.
<!--more-->

Und was macht man mit solch einem Feed? Früher&trade; nahmen wir eine Feedreader Software und abonnierten dort solche Feeds. Der [Google Reader](https://de.wikipedia.org/wiki/Google_Reader) war, bis zu seiner Einstellung, die beste Software der Welt. In diesen Readern werden dann die Einträge der abonnierten Seiten gezeigt, wir haben also alle unsere Interessen an einer Stelle vereint und müssen nicht x verschiedene Seiten einzeln aufrufen. Das ganze ist dem Facebook Newsfeed oder der Twitter Timeline gar nicht mal so unähnlich, hat aber einen gewaltigen Vorteil, der Reader zeigt (wenn er denn so programmiert ist) uns alles und alles chronologisch an. Kein Algorithmus entscheidet darüber, was an erster Stelle steht und uns bleibt nichts verborgen, weil der Algorithmus meint es wäre weniger wichtig.

So gesehen sind Feeds, gerade in unseren "postfaktischen Zeiten", eigentlich eine tolle Technologie, aber wahrscheinlich sind sie nicht einfach genug. Feedreader gibt es, als Nischenprodukt, auch heute noch, ich selbst nutze mittlerweile [Feedly](https://feedly.com). Solltest du schon mal einen Podcast abonniert haben, die Technologie dahinter sind auch RSS Feeds (um einen weiteren Anwendungsfall zu nennen).

## Die Überschrift lautet "Ein RSS Reader in Python", nicht "Gelaber über Feeds"!!!einself

Ist ja gut, kommt ja schon. Aber um deine Wut noch mehr zu provozieren: Die Überschrift ist eine maßlose Übertreibung. Wir werden keinen feature-complete RSS Reader bauen, sondern nur eine kleine Seite, welche einen vorgegebenen Feed nimmt, ein paar Informationen ausliest und diese präsentiert.

Die Seite selbst benutzt [Flask](http://flask.pocoo.org/docs/0.12/quickstart/), das Installieren von Packages in Python (und die daraus resultierenden Herausforderungen bzgl. virtual environments) waren in der Vergangenheit immer eine Spur komplexer, als zwingend nötig. Die, aktuell, empfohlene Vorgehensweise ist die Benutzung von [Pipenv](https://github.com/pypa/pipenv).

Mit Pipenv muss kein virtual environment mehr explizit erstellt werden, dieses wird mit der ersten Installation eines Packages automatisch erstellt. Mittels `pipenv shell` wird es aktiviert. Danach legen wir eine Datei `app.py` an und setzen eine Umgebungsvariable für das Flask CLI (Achtung: Windowssyntax)

```
> pipenv install flask
[...]

> pipenv shell
Launching subshell in virtual environment. Type 'exit' to return.

> touch app.py

> set FLASK_APP=app.py
```

Die gewünschten Informationen aus dem Feed sollen der Feedname, der Author und der neuste Eintrag sein. BLABLA

{% raw %}
```django
<!doctype html>
<title>Feedreader</title>

<p>
  <strong>Feed:</strong> \{{ data.name }}x
</p>

<p>
  <strong>Author:</strong> {{data.autor}}
</p>

<p>
  <strong>Neuster Beitrag:</strong>
  <div>
    {{data.entry}}
  </div>
</p>
```
{% endraw %}

bla bla

```python
from flask import Flask, render_template
app = Flask(__name__)

@app.route('/')
def index():
    data = { 'name': 'Test', 'autor': 'John Doe', 'entry': 'lorem ipsum'}
    return render_template('index.html', data=data)
```

Bla bla

![Es funktioniert]({{ site.url }}/assets/images/blog/2018/feedreader_first.png)
