---
id: 247
title: 'Python installieren Mac | Anleitung 2022'
date: '2022-01-27T18:20:23+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=247'
permalink: /2022/01/27/python-installieren-mac-anleitung-2022/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2022/01/installieren-mac.jpg'
categories:
    - Linux
    - MacOS
    - 'MacOS und Linux'
tags:
    - Python
---

**Hallo und herzlich Willkommen zurück. Ich bin Chris und zeig euch heute wie man Python auf einem Mac installiert. Dieser Artikel richtet sich an absolute Anfänger. Wenn du noch nie mit Python gearbeitet hast, bist du hier genau richtig.** **Und, weil oftmals die Frage kommt noch eine Sache vorab: Alles was hier machen ist natürlich komplett kostenlos.**

<figure class="wp-block-embed is-type-video is-provider-youtube wp-block-embed-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" frameborder="0" height="387" loading="lazy" src="https://www.youtube.com/embed/JknlXYx5zwI?feature=oembed" title="Python installieren MAC 🍏 |  Tutorial für Anfängerinnen und Anfänger | (Apple, Deutsch)" width="688"></iframe></div></figure>Das ist unsere kleine To-Do Liste für heute:

1. Terminal starten
2. Homebrew einrichten
3. Python installieren
4. Python starten

Als allererstes werden wir das **Terminal** starten. Das Terminal ist sozusagen unsere Kommandozentrale, mit der wir unseren Computer steuern können.

Danach installieren wir **Homebrew**. Homebrew widerum hilft uns, Pakete (Programme) für den Mac zu installieren.

Als nächstes installieren wir **Python** und zum Abschluss starten wir Python natürlich noch, um zu sehen, ob alles gut funktioniert hat.

## Terminal starten

Legen wir also los mit dem Terminal. Dafür drücken wir *Command* und die *Leertaste* gleichzeitig. Daraufhin geht die Spotlight-Suche an und da tippen wir jetzt einfach „Terminal“ ein. Wir bestätigen das mit *Enter* und schon ist das Terminal offen. Mit dem Terminal können wir dem Computer jetzt Befehle geben.

## Homebrew installieren

Als nächstes installieren wir jetzt Homebrew. Dafür gehen wir einfach auf die [Website von Homebrew](https://brew.sh/index_de).

Von der Website kopieren wir uns diesen Installationscode hier raus.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
```

</div>Den Code nehmen wir jetzt mit in unser Terminal, fügen ihn ein und drücken *ENTER*. Jetzt geben wir unser Passwort ein und bestätigen wieder mit *ENTER*.

## Python installieren mit Homebrew

Ihr könnt nach einigen Minuten jetzt sehen, dass Homebrew erfolgreich installiert wurde. Und jetzt können wir mithilfe von Homebrew endlich Python installieren.

Dafür geben wir unten einen Befehl ein.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-bash" data-lang="Bash">```
brew install python3
```
```

</div>Und jetzt können wir auch schon probieren, Python zu starten. Dafür tippen wir einfach ein:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-bash" data-lang="Bash">```
python3
```
```

</div>Wie ihr seht startet jetzt Python und wir können Python ab sofort auf unserem Computer nutzen. So sollte euer Terminal dann aussehen:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-bash" data-lang="Bash">```
Chris@MacBook-Air ~ % python3
Python 3.9.10 (main, Jan 15 2022, 11:40:53) 
[Clang 13.0.0 (clang-1300.0.29.3)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 

```
```

</div>Wenn ihr wollt, stellt mir gern eure Fragen in der Kommentarspalte, ich versuche dann mit kurzen Videoantworten zu antworten. Ansonsten wünsch ich euch jetzt noch ganz viel Spaß mit Python, bleibt neugierig und bis bald!