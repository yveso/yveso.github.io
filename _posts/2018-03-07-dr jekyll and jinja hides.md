---
layout: post
title: Dr. Jekyll and Jinja hides
---

> Jekyll uses the Liquid templating language to process templates.
>
> <cite>[Jekyll Docs: Templates](https://jekyllrb.com/docs/templates/)</cite>

Das ist eine tolle Sache, führt aber zu Problemen, wenn man über eine eine andere Template Sprache (wie Jinja2) schreiben möchte. Schreibt man beispielsweise folgendes in einem Markdown Dokument:

![Ohne raw Tag]({{ site.url }}/assets/images/blog/2018/jekyll_raw_without.png)

So ist der gerenderte Output wie folgt, Tags und Objekte fehlen in der Darstellung, da die Jinja2 fälschlicherweise als Liquid interpretiert wird.

```django
{% if name %}
<h1>Hello {{ name }}!</h1>
{% else %}
<h1>Hello, World!</h1>
{% endif %}
```

Der Retter in der Not ist der [`raw` Tag](http://shopify.github.io/liquid/tags/raw/). Mit diesem lässt sich die Verarbeitung von Liquid Tags unterbinden.

![Mit raw Tag]({{ site.url }}/assets/images/blog/2018/jekyll_raw_with.png)

Tada:

{% raw %}
```django
{% if name %}
<h1>Hello {{ name }}!</h1>
{% else %}
<h1>Hello, World!</h1>
{% endif %}
```
{% endraw %}
