---
id: 86
title: 'Kleinste und größte Werte einer Liste finden mit Python'
date: '2021-09-26T07:50:59+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=86'
permalink: /2021/09/26/kleinste-und-groesste-werte-einer-liste-finden-mit-python/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/09/thumbnail-werte-finden.png'
categories:
    - 'Daten auswerten'
tags:
    - Python
---

<figure class="wp-block-embed is-type-video is-provider-youtube wp-block-embed-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" frameborder="0" height="387" loading="lazy" src="https://www.youtube.com/embed/p45SuBIvUg0?start=117&feature=oembed" title="Python: Kleinste und größte Werte finden 🐍 | Tutorial für Anfängerinnen und Anfänger (Deutsch, 2021)" width="688"></iframe></div></figure>Mein Zuschauer *PyQGis* hat gefragt, wie herausfinden kann, an welcher Position sich das kleinste Element einer Liste befindet. Um das Problemchen zu lösen, müssen wir eigentlich nur zwei Dinge tun. Wir müssen zuerst das kleinste Element finden und in einem zweiten Schritt dessen Position ermitteln. Ihr seht, ich hab hier schon eine Liste angelegt. Die heißt einfach `coole_liste`:

`coole_liste = [29, 87, 467, 2, 57]`

In Python können wir uns das kleinste Element über die Funktion `min()` anzeigen lassen. Dafür schreibe ich:

`min(coole_liste)`

Diesen Wert will ich später noch verwenden, deshalb gebe ich ihm einen Namen.

`kleinster_wert = min(coole_liste)`

Und jetzt schauen nach, wo sich das Element befindet. Daür nutzen wir die `index`– Funktion. Und die funktioniert so: Ich gebe zuerst die Liste an, um die es geht, dann das Wort `index` und dann den Wert, dessen Position ich finden möchte.

`coole_liste.index(kleinster_wert)`

Und auch diesen Wert will ich in einer Variable speichern.

`pos_min = coole_liste.index(kleinster_wert)`

Und jetzt kann ich mir das Ganze auch schon ausgeben lassen. Das funktioniert übrigens genauso einfach mit der größten Zahl. Dafür muss ich einfach statt der `min()`-Funktion die `max()-Funktion nutzen. Unser fertiger Quellcode sieht jetzt so aus:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
coole_liste = [29, 87, 467, 2, 57]

kleinster_wert = min(coole_liste)
groesster_wert = max(coole_liste)

pos_min = coole_liste.index(kleinster_wert)
pos_max = coole_liste.index(groesster_wert)

print(pos_min, pos_max)
```
```

</div>