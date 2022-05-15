---
id: 69
title: 'Tutorial: NASA-Daten mit Python auslesen'
date: '2021-09-22T15:37:25+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=69'
permalink: /2021/09/22/tutorial-nasa-daten-mit-python-auslesen/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/09/thumbnail-nasa-1.png'
categories:
    - API
---

<figure class="wp-block-embed is-type-video is-provider-youtube wp-block-embed-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" frameborder="0" height="387" loading="lazy" src="https://www.youtube.com/embed/fOPWZytYsFM?start=1&feature=oembed" title="Python API Tutorial (Deutsch) | 🚀 Für Anfängerinnen und Anfänger | NASA-API" width="688"></iframe></div></figure>Im heutigen Tutorial sollte sich eigentlich alles um den Mars drehen. Ich wollte euch heute nämlich eigentlich zeigen, wie man mit Hilfe eines Python Skriptes das aktuelle Wetter auf dem Mars auslesen kann. Aber wie das immer so ist: Der NASA sind ihre Sensoren um die Ohren geflogen und deshalb gibt es bis auf weiteres keine Daten mehr, und somit auch kein Wetterbericht vom Mars.

Die gute Neuigkeit: Auch auf der Erde gibt es über Daten der Nasa mehr als genug spannende Sachen zu entdecken. Und genau das machen wir heute. Ich bin Chris, und das ist Programmieren mit Chris. Viel Spaß.

Die Nasa stellt viele ihrer Daten öffentlich über eine sogenannte API zur Verfügung. So eine API ist eine Schnittstelle zwischen uns und einem Datenanbieter, also z.B. der Nasa.

Auf der Website der Nasa finden wir sogar gleich eine ganze Menge von verschiedenen APIs, mit denen man jeweils andere Daten abrufen kann. Für uns ist heute die **EONET API** interessant. Die sammelt alle größeren Naturereignisse auf der Erde, also Zyklone, Waldbrände oder auch Vulkanausbrüche. Und als kleines Beispiel schreiben wir heute ein Skript, das uns alle Ereignisse innerhalb des letzten Jahres anzeigt.

Wir beginnen damit, dass wir uns die benötigten Module installieren. Dafür gehe ich in mein Terminal und tippe ein:

`pip3 install requests`

Das Modul ist installiert und wir können es jetzt importieren.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import requests
import json
```
```

</div>Als nächstes stellen wir eine Anfrage an den Server der Nasa. Und damit wir die Anfrage auf die richtige Art und Weise stellen, müssen wir uns anschauen, was für eine Anfrage der Server der Nasa erwartet. Informationen zur Funktionsweise einer API stehen normalerweise in der sogenannten API-Dokumentation.

<https://eonet.sci.gsfc.nasa.gov/docs/v2.1>

Und in den meisten Dokumentationen finden wir Beispielanfragen wie diese hier:

<https://eonet.sci.gsfc.nasa.gov/api/v2.1/events>

So eine API Anfrage siehst erstmal aus wie eine Internetadresse, enthält aber zusätzlich einige Parameter. Parameter sind Schlüsselwörter, die wir an die Anfrage einfach mit ranhängen können. Und mit denen sagen wir dem Server, was genau wir an Daten anfragen wollen. Zwei Parameter sind für uns besonders interessant: `limit` und `days`. Mit `limit` legen wir fest, wieviele Ergebnisse wir haben wollen. Und mit `days` können wir (wenig überraschend) festlegen, für wieviele Tage wir die Daten haben möchten.

Beide Parameter können wir schon einmal in unserem Skript aufschreiben.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
limit = 500
days = 356
```
```

</div>Und wenn wir schon dabei sind, nehmen wir uns auch schon mal diese Beispielanfrage mit.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
url = https://eonet.sci.gsfc.nasa.gov/api/v2.1/events?limit=5&days=20&source=InciWeb&status=open
```
```

</div>Und damit Python weiß, dass es sich um eine Zeichenkette handelt, schreiben wir vor die Adresse ein f und setzen die gesamte Adresse in Anführungsstrichen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
url = f'https://eonet.sci.gsfc.nasa.gov/api/v2.1/events?limit=5&days=20&source=InciWeb&status=open'
```
```

</div>Jetzt ersetzen wir die Parameter, die schon in der Adresse stehen durch unsere eigenen Werte.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
url = f'https://eonet.sci.gsfc.nasa.gov/api/v2.1/events?limit={limit}&days={days}'
```
```

</div>Unsere Anfrage ist startklar und jetzt schicken wir sie an den Server der Nasa.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
r = requests.get(url)
```
```

</div>Antwort des Servers: `<Response [200]>`

Damit wir das, was uns der Server zurückgeschickt hat, lesen können, wandeln wir die Serverantwort in das JSON-Format um. JSON ist ein besonders einfaches, leicht lesbares Format, das wir gleich leicht durchsuchen können.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
events_data = r.json()
```
```

</div>Diese Daten speichern wir uns auch gleich in einer eigenen json-Datei, damit sie nicht verloren gehen. Dafür öffnen wir zunächst eine neue Datei und sagen, dass wir in der Datei schreiben wollen:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
with open('events.json','w') as f:
```
```

</div>Und während die Datei offen ist, schreiben wir in sie unsere Daten.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
f.write(json.dumps(events_data, indent=4))
```
```

</div>Mit dem Begriff `dumps` werden unsere Daten in eine JSON-Zeichenkette umgeformt. Und mit `indent=4` legen wir fest, wie groß die Einrückungen zwischen den einzelnen Elementen sein sollen.

In der JSON Datei suchen wir jetzt nach dem Teil der Daten, der uns interessiert. Einzelne Objekte werden bei JSON durch geschwungene Klammern gekennzeichnet. Und die Objekteigenschaften können wir an den Anführungszeichen erkennen. Wir können hier jetzt sehen, dass unsere json Datei ein Objekt enthält (das sehen wir an der ersten Klammer) und dieses Objekt hat verschiedene Eigenschaften. Es hat z.B. einen Titel und eine Beschreibung.

Für uns ist jetzt vor allem die Eigenschaft `events `interessant. `events `enthält nämlich selbst wieder Objekte, was ihr an den geschwungenen Klammern erkennen könnt. Und diese Objekte sind genau das, was wir suchen, weil jedes Objekt in Events für ein Ereignis steht, das dokumentiert wurde, also z.B. einen Vulkanausbruch oder einen Waldbrand. In jedem Fall ist also schon mal der Teil `events`für uns der spannende, deshalb speichern wir uns Events schon mal in einer eigenen Variable.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
event_list = events_data['events']
```
```

</div>Und jetzt folgt schon der letzte Schritt. Wir lassen uns jetzt alle Elemente der Liste ausgeben.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
for event in event_list:
    print(event['title'])
```
```

</div>Okay, soviel erstmal für heute. Viel Spaß beim Ausprobieren, bleibt neugierig und bis bald!

## [](https://github.com/chrischma/ProgrammierenMitChris#-kompletter-quellcode)✅ Kompletter Quellcode

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import requests
import json

limit = 500
days = 356

url = f'https://eonet.sci.gsfc.nasa.gov/api/v2.1/events?limit={limit}&days={days}'
r = requests.get(url)
events_data = r.json()
event_list = events_data['events']

# with open('events.json','w') as f:
#    f.write(json.dumps(events_data, indent=4))

for event in event_list:
		# print(event)
    if 'fire' in str(event['categories']):
        print(event['title'])
```
```

</div>