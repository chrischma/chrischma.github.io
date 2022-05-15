---
id: 274
title: "Unser erster Webscraper |\_Python Tutorial (Deutsch)"
date: '2022-02-18T15:31:30+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=274'
permalink: /2022/02/18/unser-erster-webscraper/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2022/02/Thumbnail-webscarping.jpg'
categories:
    - 'Bots und Automatisierung'
    - MacOS
tags:
    - Python
    - Web-Scraper
    - Web-Scraping
    - Webscraping
---

Wenn ihr wissen wollt, wie man Daten aus einer Website mit Python auslesen kann, dann seid ihr hier genau richtig.

<figure class="wp-block-embed is-type-video is-provider-youtube wp-block-embed-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" frameborder="0" height="387" loading="lazy" src="https://www.youtube.com/embed/IFJq_cXR2lU?feature=oembed" title="Python: Unser erster Web-Scraper | Tutorial für Anfängerinnen und Anfänger | Deutsch (2022)" width="688"></iframe></div></figure>Ich zeige euch das heute an einem ganz einfachen Beispiel, das Prinzip lässt sich aber auf alle möglichen Websiten übertragen.

## Module installieren

Wir beginnen wie immer damit, dass wir die alle Module installieren, die wir heute brauchen. Ich zeige euch hier die Installation über die Konsole. Das ist in der Regel die schnellste und bequemste Art. Ihr könnte die Module aber natürlich auch von Hand installieren. Die Links dazu stelle ich euch in die Videobeschreibung.

Das erste Modul, das wir brauchen werden nennt sich requests. Damit kann man mit Python eine Internetseite aufrufen und sich die Daten zurückgeben lassen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
`pip3 install requests
```
```

</div>Außerdem werden wir das Modul BeautifulSoup benötigen. Das macht es uns möglich, die gesammelten Daten dann zu sortieren und uns genau die Daten herauszusuchen, die wir wirklich brauchen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
pip3 install beautifulsoup4
```
```

</div>## Skript anlegen

Wir sind jetzt soweit startklar und können unser Skript anlegen. Für das Schreiben des Skriptes könnt ihr jeden beliebigen Texteditor verwenden, ich benutze jetzt hier SublimeText.

\[Datei anlegen ’sonnenaufgang.py‘\]

## Module importieren

Ganz oben im Skript importieren wir jetzt die Module, die wir gerade installiert haben.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import requests                 
from bs4 import BeautifulSoup
```
```

</div>Und dann können wir auch schon mit dem eigentlichen Webscraping beginnen. Für unser Beispiel habe ich heute mal die Website Sonnenaufgang.online ausgesucht. Da kann man eine Stadt eingeben und kriegt dann allerhand interessante Sonnendaten aufgelistet. Und wir wollen heute mal beispielhaft auslesen, wann in Leipzig die Sonne aufgeht.

Das ist also unsere Seite, die wir auslesen wollen. Und von der können wir uns gleich mal die URL rauskopieren und mit in unser Skript nehmen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
URL = 'https://sonnenaufgang.online/sun/leipzig'
```
```

</div>Und jetzt geben wir Python den Befehl, diese Website aufzurufen und die Daten, die die Website zurückgibt, zu speichern.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
response = requests.get(URL)
```
```

</div>Jetzt interessieren uns aber nunmal nicht alle Daten der Website, sondern wir wollen nur ganz bestimmte Sachen auslesen. Und deshalb nutzen wir jetzt BeautifulSoup, um die Antwort der Website zu durchsuchen. Dafür legen wir zuerst ein Soup-Objekt an.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
soup = BeautifulSoup(response.text, 'html.parser')
```
```

</div>Und jetzt kommt auch schon der schwierigste Part. Wir müssen jetzt nämlich herausfinden, wie genau der Bereich der Website heißt, wo sich der Datensatz befindet, den wir haben wollen. Dafür nutzen wir die Entwicklerkonsole. Damit können wir sozusagen hinter die Kulissen einer Website schauen und uns angucken, wie die Website im Quellcode aufgebaut ist. So eine Entwicklerkonsole hat eigentlich jeder moderner Browser. (Bei Google Chrome über \[…\] -&gt; Weitere Tools -&gt; Entwicklertools)

Mit dem Pfeilsymbol kann ich jetzt Bereiche auf der Website markieren und herausfinden, wie die im Quelltext benannt sind. Und hier kann ich jetzt sehen, dass mein Datensatz ein span-Objekt ist. Und weil es von solchen span-Objekten in der Regel sehr sehr viele gibt, schauen wir mal noch, welche Eigenschaft genau diese Objekt hat, was wir haben wollen. Und da können wir sehen, dass das einen data-name hat, und der ist sunrise. Und genau danach suchen wir jetzt mit unserem Python Skript.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
sunrise_data = soup.find('span', {'data-name': 'sunrise'})

```
```

</div>Das funktioniert jetzt eigentlich schon gut, aber wir machen das ganze jetzt mal noch etwas hübscher. Und zwar entfernen wir jetzt mal die Sekundenangabe ganz am Ende.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
sunrise_text = sunrise_data.text[:-3]
```
```

</div>So, und jetzt können wir uns den ganzen Bumms auch schon ausgeben lassen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
print(f'Die Sonne geht heute um {sunrise_text} Uhr auf.')
# Ergebnis: Die Sonne geht heute um 07:20 Uhr auf.

```
```

</div>## Fazit 

Ich hoffe ich konnte mit diesem Video bei euch ein bisschen für Klarheit sorgen. Ich kann auf jeden Fall sagen: Webscraping ist echt ein super spannendes Thema. Und wenn man die Grundlagen einmal kapiert hat, dann geht alles weitere wirklich einfach von der Hand.

Wenn ihr weitere Fragen habt, schreibt sie mir gern in die Kommentare. Ansonsten wünsch ich euch noch einen wunderschöne Woche, bleibt neugierig und bis bald!

## ✅ Kompletter Quellcode

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import requests
from bs4 import BeautifulSoup

URL = 'https://sonnenaufgang.online/sun/leipzig'

response = requests.get(URL)

soup = BeautifulSoup(response.text, 'html.parser')
sunrise_data = soup.find('span', {'data-name': 'sunrise'})
sunrise_text = sunrise_data.text[:-3]

print(f'Die Sonne geht heute um {sunrise_text} Uhr auf.')

```
```

</div>