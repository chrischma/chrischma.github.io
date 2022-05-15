---
id: 6
title: 'Python: Passwörter sicher speichern (außerhalb von Skripten) (MacOS / Linux)'
date: '2021-08-11T07:06:06+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=6'
permalink: /2021/08/11/python-passwoerter-sicher-speichern-ausserhalb-von-skripten-macos-linux/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/08/Thumbnail-passw.png'
categories:
    - 'MacOS und Linux'
---

Heute schauen wir uns an, wie man Passwörter außerhalb von Skripten speichern kann.

<figure class="wp-block-embed is-type-video is-provider-youtube wp-block-embed-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" frameborder="0" height="387" loading="lazy" src="https://www.youtube.com/embed/nZyxw3ayEyA?feature=oembed" title="Python: Passwörter und Keys sicher speichern (außerhalb von Skripten) (MacOS) | Tutorial (Deutsch) 🔑" width="688"></iframe></div></figure><div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import requests
​
API_KEY = "e1b8c7307dfc5d97e974as71350f44f8ab7"
​
city = input("Hallo! Bitte gib eine Stadt ein.")
url = f'https://api.openweathermap.org/data/2.5/weather?q={city}&appid={API_KEY}&units=metric'
​
data = requests.get(url).json()
temp = data['main']['temp']
humidity = data['main']['humidity']
​
print(f'In {city} beträgt die Temperatur {temp}. Die Luftfeuchtigkeit beträgt {humidity}%.')
```
```

</div>Es ist immer mal wieder notwendig, dass ein Python Skript Zugriff auf sensible Daten bekommt. Das können Passwörter sein, aber auch z.B. API Keys oder Zugangsdaten zu einer Datenbank. Schauen wir uns kurz ein Beispiel an, das wir für ein anderes Tutorial schon mal geschrieben haben.

Unser Skript hat ein entscheidenes Problem: Wenn wir diesen API-Code jetzt beispielsweise auf Github teilen würden, wäre unser API Key für alle sichtbar im Netz. Und das wollen wir natürlich nicht.

Es gibt dafür aber eine bequeme Lösung. Die Idee ist, dass wir den API Key lokal, also auf unserem Rechner speichern und dann einfach in das Skript importieren, wenn wer gebraucht wird. Und dafür nutzen wir die .bash\_profile-Datei. Dafür gehen wir zunächst ins Terminal und geben diesen Befehl ein:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
nano .bash_profile 
```
```

</div>Damit starten wir den Nano-Texteditor und öffnen mit ihm die Datei `.bash_profile`. In dieser Datei können wir jetzt unseren API-Key hinterlegen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
export wetter_api_key="e1b8c7307dfc5d97e974as71350f44f8ab7"
```
```

</div>Jetzt können wir die Datei auch schon verlassen. Dafür drücke ich Command+X und anschließend Y und dann Enter. Damit unsere Änderungen jetzt auch wirksam werden, führen wir noch folgenden Befehl aus:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
source .bash_profile
```
```

</div>Jetzt testen wir kurz aus, ob der API-Key auffindbar ist. Dafür lassen wir uns den Key im Terminal ausgeben:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
echo $wetter_api_key<br>-> e1b8c7307dfc5d97e974as71350f44f8ab7
```
```

</div>Weiter geht’s im Quellcode. Um auf die Datei zuzugreifen, die wir gerade erstellt haben, nutzen wir das Modul os. Und greifen dann auf unseren Key zu.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
import os
API_KEY = os.environ.get('wetter_api_key')
```
```

</div>Okay, probieren wir das Ganze aus!

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
python3 weather.py
Hallo! Bitte gib eine Stadt ein.Leipzig
In Leipzig beträgt die Temperatur 17.08. Die Luftfeuchtigkeit beträgt 79%.
```
```

</div>Okay, soviel erstmal für heute. Fragen und Wünsche könnt ihr wie immer in der Kommentarspalte dalassen, ich antworte bei passenden Fragen mit kurzen Videoantworten. Und jetzt viel Spaß beim Ausprobieren, bleibt neugierig und bis bald!

✅ Hier noch einmal der komplette Quellcode:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import requests
import os

API_KEY = os.environ.get('wetter_api_key')

city = input("Hallo! Bitte gib eine Stadt ein.")
url = f'https://api.openweathermap.org/data/2.5/weather?q={city}&appid={API_KEY}&units=metric'

data = requests.get(url).json()
temp = data['main']['temp']
humidity = data['main']['humidity']

print(f'In {city} beträgt die Temperatur {temp}. Die Luftfeuchtigkeit beträgt {humidity}%.')
```
```

</div>