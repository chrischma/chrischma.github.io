---
id: 66
title: 'Python Threading &#8211; Mehrere Funktionen parallel ausführen'
date: '2021-09-22T15:25:56+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=66'
permalink: /2021/09/22/python-threading-mehrere-funktionen-parallel-ausfuehren/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/09/Thumbnail-threading.png'
categories:
    - Datenbanken
    - Effizienz
---

Wenn ihr wissen wollt. wie man mit Python mehrere Funktionen parallel ausführen kann, dann seid ihr hier genau richtig. Ich bin Chris und das ist Programmieren mit Chris – viel Spaß.

<figure class="wp-block-embed is-type-video is-provider-youtube wp-block-embed-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" frameborder="0" height="387" loading="lazy" src="https://www.youtube.com/embed/WmpI4iwg00U?feature=oembed" title="Python - Mehrere Funktionen parallel laufen lassen | Tutorial (Deutsch) | Threading | Anfänger ⛓️" width="688"></iframe></div></figure>Normalerweise läuft ein Python Programm Schritt für Schritt ab. Python schnappt sich also die erste Aufgabe, arbeitet sie ab und geht dann zur nächsten Aufgabe weiter. Man sagt auch, dass Python in einem sogenannten Thread, also in einem Kanal oder Gang läuft.

Das Schöne ist, dass wir mehrere dieser Threads erstellen können, wenn wir wissen wie. Und genau dafür nutzen wir das Modul THREADING.

Schauen wir uns an, wie das in der Praxis funktioniert.

Als erstes Schreiben wir ein kleines Programm, das aus zwei einfachen Funktionen besteht. Die beiden Funktionen sollen nichts anderes machen als immer wieder sagen, dass sie gerade laufen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import time


def funktion_1():
    while True:
        print("Funktion 1 läuft")
        time.sleep(1)

        
def funktion_2():
    while True:
        print("Funktion 2 läuft")
        time.sleep(2)
        
        
funktion_1()
funktion_2()
```
```

</div>Wenn wir das Skript jetzt abfeuern, stellen wir fest, dass nur die erste Funktion aufgerufen wird. Und das liegt daran, dass Python die Funktion erst zuende aufrufen möchte, bevor Python weiter zur zweiten Funktion geht. Da können wir jetzt aber bis uns graue Haare wachsen, weil die erste Funktion ja unendlich lange ausgeführt wird.

Machen wir uns deshalb jetzt daran, die beiden Funktionen gleichzeitig auszuführen. Dafür nutzen wir das Threading Modul. Das ist vorinstalliert, wir können es also direkt importieren und nutzen.

`from threading import Thread`

Jetzt definieren wir einen neuen Thread und legen fest, welche Funktion in diesem Thread laufen soll. Das gleiche machen wir auch gleich für die zweite Funktion.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
thread_1 = Thread(target=funktion_1)
thread_2 = Thread(target=funktion_2)
```
```

</div>Jetzt haben wir es fast geschafft. Wir müssen die Threads nur noch starten.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
thread_1.start()
thread_2.start()
```
```

</div>Okay, soviel erstmal für heute. Fragen und Wünsche könnt ihr wie immer in der Kommentarspalte dalassen, ich antworte bei passenden Fragen mit kurzen Videoantworten. Wenn ihr den Kanal unterstützen wollt, dann findet ihr alle Infos dazu in der Videobeschreibung. Und jetzt viel Spaß beim Ausprobieren, bleibt neugierig und bis bald!

## [](https://github.com/chrischma/ProgrammierenMitChris#-kompletter-quellcode)✅ Kompletter Quellcode

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import time
from threading import Thread


def funktion_1():
    while True:
        print("Funktion 1 läuft")
        time.sleep(1)


def funktion_2():
    while True:
        print("Funktion 2 läuft")
        time.sleep(1)


thread_1 = Thread(target=funktion_1)
thread_2 = Thread(target=funktion_2)

thread_1.start()
thread_2.start()
```
```

</div>