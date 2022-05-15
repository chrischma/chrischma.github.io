---
id: 393
title: 'Komplette Website herunterladen mit einem Befehl'
date: '2022-05-14T05:45:44+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=393'
permalink: /2022/05/14/komplette-website-herunterladen-mit-einem-befehl/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2022/05/Thumbnail-wget-name.png'
categories:
    - Linux
    - MacOS
tags:
    - Crawler
    - Download
    - Linux
    - MacoS
    - Terminal
    - wget
---

<figure class="wp-block-image size-large">[![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/05/Thumbnail-wget-name-1024x576.png)](https://youtu.be/5S_2PmMFBug)</figure>Hallo und ganz herzlich willkommen zurück! In diesem Artikel möchte ich euch einen Befehl zeigen, mit dem ihr super bequem eine komplette Website mitsamt aller Inhalte herunterladen könnt.

Für Ungeduldigen unter euch kommt jetzt gleich der Befehl, für alle Neugierigen hab ich dann im Anschluss noch eine kleine Erklärung vorbereitet, wie es funktioniert.

Der Befehl sieht folgendermaßen aus:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-bash" data-lang="Bash">```
wget [Link zur Website] -r

(z.B. wget http://christoph-schmalfuss.de/ -r)
```
```

</div>Ich brauch dann nur noch ENTER drücken und die Website wird in das Verzeichnis heruntergeladen, in welchem ich mich gerade mit meinem Terminal befinde. Das geht also schon mal eeecht unkompliziert, schauen wir uns mal etwas genauer an, was ich hier eigentlich eingetippt habe. Unser Befehl besteht aus drei Teilen. Und zwar aus dem Wort „wget“, dem Link zu meiner Website und dem Parameter -r.

## Was ist wget?

wget ist erstmal ein Open Source Command-Line Tool, das das einfache Herunterladen von Daten von Websiten bzw. Servern ermöglicht. Und mit dem wget rufen wir dieses Tool einfach auf.

In vielen Linux Versionen ist wget übrigens schon vorinstalliert. Auf MacOS bietet sich die Installation über Homebrew an. Dafür müssen wir nur einmal den folgenden Befehl aufrufen und wget ist dann dauerhaft installiert und nutzbar.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-bash" data-lang="Bash">```
brew install wget
```
```

</div>Falls ihr Homebrew noch nicht installiert haben solltet, verlinke ich euch [hier](https://brew.sh) auch noch einmal den Link zu Homebrew.

## Was bedeutet „-r“? 

Neben dem Wort wget und dem Link zu unserer Website hatte unserBefehl ja noch einen dritten Bestandteil und zwar das -r. Und das -r steht einfach für „rekursiv“. Wir sagen damit also wget, dass es die Website rekursiv runterladen soll. wget soll also nicht nur die eine Website runterladen, die wir als angegeben haben, sondern soll sozusagen durch alle Unterseiten der Website durchwandern und alle Unterseiten, die es findet, ebenfalls herunterladen.

Neben dem Parameter -r gibt es aber natürlich auch noch eine Menge anderer Optionen, die wir mit wget nutzen können. Wir können z.B. mit dem Parameter -A angeben, welche Dateitypen wir herunterladen wollen. So kann ich mir z.B. nur die Bilder einer Website herunterladen indem ich schreibe:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-bash" data-lang="Bash">```
wget http://christoph-schmalfuss.de/ -A .png -r
```
```

</div>Wenn ihr ein bisschen tiefer in das Thema der Parameter einsteigen wollt, verlink ich euch [hier](https://wiki.ubuntuusers.de/wget/#Aufruf) auch nochmal die vollständige Liste der Optionen, die wget bietet.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
https://wiki.ubuntuusers.de/wget/#Aufruf
```
```

</div>Ich kann euch sehr empfehlen, euch dafür einfach mal ein paar Minuten Zeit zu nehmen und die für euch relevantesten Befehle auszuprobieren. Von mir soll’s das für heute gewesen sein, ich wünsch euch viel Freude beim Entdecken, bleibt neugierig und bis bald.