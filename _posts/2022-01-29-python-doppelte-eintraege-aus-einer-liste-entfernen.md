---
id: 254
title: 'Python &#8211; Doppelte Einträge aus einer Liste entfernen'
date: '2022-01-29T12:28:56+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=254'
permalink: /2022/01/29/python-doppelte-eintraege-aus-einer-liste-entfernen/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2022/01/Thumbnail-duplikate.jpg'
categories:
    - 'Daten auswerten'
    - Effizienz
    - 'Kurze Tipps'
tags:
    - Dictionary
    - Python
---

<figure class="wp-block-image size-large">![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/02/Thumbnail-duplikate-1024x576.jpg)</figure>Hier kommt ein kleiner Python Trick, mit dem man Duplikate aus einer Liste entfernen kann. Nehmen wir an wir haben so eine Liste wie diese hier. In der Liste befinden sich einfach ein paar hübsche europäische Städte, blöderweise kommen aber in der Liste einige Städte doppelt vor.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
meine_liste = ['Paris', 'Rome', 'London', 'London', 'Berlin', 'Barcelona', 'Amsterdam', 'Amsterdam', 'St. Petersburg', 'Istanbul', 'Athens']

```
```

</div>Um die doppelten Einträge zu entfernen machen wir jetzt folgendes:

Als erstes wandeln wir die Liste in ein Dictionary um. Warum wir das machen, ergibt sich gleich. So ein Dictionary besteht einfach gesagt aus Paaren, die immer aus einem Schlüssel und einem Wert bestehen. Und Dictionaries haben die praktische Eigenschaft, dass Schlüssel niemals doppelt vorkommen können. Das heißt: Wenn wir aus unserer Liste ein Dictionary machen, werden die Duplikate automatisch rausgeschmissen, einfach weil Dictionaries doppelte Werte nicht erlauben.

In der Praxis nutzen wir dafür jetzt den Befehl dict.fromkeys(). Der erzeugt aus einer Liste von Keys ein Dictionary.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
mein_dict = dict.fromkeys(meine_liste)
```
```

</div>Wir wollen als Ergebnis jetzt aber eine Liste haben und deshalb wandeln wir das neue Dictionary jetzt einfach wieder in eine Liste um. Das geht mit dem Befehl list().

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
mein_dict = dict.fromkeys(meine_liste)
meine_liste = list(mein_dict)

print(meine_liste)
```
```

</div><div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
# Ergebnis: 
['Paris', 'Rome', 'London', 'Berlin', 'Barcelona', 'Amsterdam', 'St. Petersburg', 'Istanbul', 'Athens']
```
```

</div>Als Ergebnis bekommen wir jetzt unsere alte Liste zurück – und zwar ganz ohne doppelte Einträge. Und damit haben wir es auch eigentlich schon geschafft. Wenn ihr wollt, könnt ihr das ganze sogar jetzt noch weiter verknappen und auf eine Zeile schreiben.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
meine_liste = list(dict.fromkeys(meine_liste))
```
```

</div>Ja und so einfach kann man also Duplikate aus Listen in Python entfernen.

Euch vielen Dank fürs Zuschauen, bleibt neugierig und bis bald!