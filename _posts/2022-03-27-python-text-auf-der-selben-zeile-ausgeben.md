---
id: 298
title: 'Python: Text auf der selben Zeile ausgeben'
date: '2022-03-27T09:35:02+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=298'
permalink: /2022/03/27/python-text-auf-der-selben-zeile-ausgeben/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2022/03/Thumbnail-zeile.jpg'
categories:
    - 'Kurze Tipps'
    - Linux
    - MacOS
    - 'MacOS und Linux'
---

Hallo und ganz herzlich willkommen zurück. Heute schauen wir uns an, wie wir Textausgaben in Python auf ein und der selben Zeile ausgeben lassen können.

<figure class="wp-block-embed is-type-video is-provider-youtube wp-block-embed-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" frameborder="0" height="387" loading="lazy" src="https://www.youtube.com/embed/d0yERRFretk?feature=oembed" title="Python: Text auf der gleichen Zeile ausgeben (Quellcode und Erklärung) | Tutorial (Einfach, Deutsch)" width="688"></iframe></div></figure>## Das Problem mit normalen print-Ausgaben

Um das Problem gleich mal zu verdeutlichen, hab ich hier mal ein kleines Countdown-Programm geschrieben.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from time import sleep


def countdown(seconds):
	while seconds != 0:
		print(seconds) 
		sleep(1)				
		seconds -= 1
	print('Done!')

countdown(3)

```
```

</div>Das Skript funktioniert auch schon ganz gut, allerdings ist die Ausgabe noch nicht richtig hübsch. Denn wenn ich das Skript jetzt ausführe, wird jede Zahl auf eine eigene Zeile geschrieben.

## So kannst du Strings auf der selben Zeile aufrufen

Um das zu ändern und den Text auf einer Zeile auszuführen, muss ich nur eine kleine Sache zu meinem Skript hinzufügen. Die print-Funktion, die für uns Sachen ausgibt, benutzt man ja meistens in ihrer einfachsten Form, also z.B. `print(seconds)`. Man kann die Ausgabe allerdings anpassen, indem man der print-Funktion einen weiteren Parameter, also eine weitere Eigenschaft mitgibt. Und die Eigenschaft nennt sich `end`. Für die Ungeduldigen unter euch zeigt ich euch gleich mal die Lösung, eine Erklärung hab ich dann allerdings auch noch und die ist wie ich finde ziemlich witzig.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
print(seconds, end='\r') # Text wird auf selber Zeile ausgegeben
```
```

</div>Wenn ich jetzt mein Skript starte, sollte mein Text auf der gleichen Zeile ausgegeben werden.

## Wie funktioniert das?

Die große Frage ist jetzt natürlich, wie das eigentlich funktioniert. Fangen wir vielleicht mal mit dem End-Parameter an. Grundsätzlich hat der erstmal die Funktion, dass er beschreibt, was Python am Ende eine Zeile für ein Zeichen hinzufügen soll. Im Normalfall ist der `end` Parameter natürlich ein Zeilenumbruch. Und es macht ja auch Sinn, weil wir am Ende eine Zeile normalerweise einfach auf den nächsten Zeile weiterschreiben wollen und deshalb eine Zeile nach unten springen.

Wir können aber, so wie wir das gerade gemacht haben, auch jedes beliebige andere Zeichen an das Ende eine Zeile setzen. Und das Zeichen, was wir in diesem Fall verwendet haben, also das `\r`, das ist der so genannte Carrige Return. Und das Zeichen lässt sich am besten verstehen, wenn wir an die Anfänge einer Tastatur zurückgehen. Denn bei der guten alten Schreibmaschine, muss man am Ende einer Zeile nicht nur nach unten springen, sondern der Schreibmaschinenwagen, der so genannte Carrige, musste wieder von rechts nach links gebracht werden. Andernfalls würde man ja auf der nächsten Zeile nicht wieder wie gewohnt links am Anfang einer Zeile weiterschreiben. Und diesen Carrige-Return also das Zurückspringen auf die Position am Anfang einer Zeile, das ist das Zeichen was wir jetzt ans Ende jeder Zeile bei Python gesetzt haben.

Das heißt, dass jedes Mal, wenn Python am Ende eine Zeile angekommen ist, Python nicht wie gewohnt nach unten springt, sondern am Beginn der Zeile weiter schreibt. Und genau das führt dann eben zu dem Effekt, den wir uns gewünscht haben, dass Python auf der selben Zeile schreibt und wir so Countdown bauen konnten. Und damit haben wir es für heute auch schon geschafft. So einfach kann man also in Python Textausgaben auf der selben Zeile ausgeben.

## ✅ Kompletter Quellcode

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from time import sleep


def countdown(seconds):
	while seconds != 0:
		print(seconds, end='\n') 
		sleep(1)				
		seconds -= 1
	print('Done!')

countdown(3)

```
```

</div>