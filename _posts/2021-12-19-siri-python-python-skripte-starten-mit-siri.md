---
id: 211
title: 'Siri &#038; Python – Python Skripte starten mit Siri'
date: '2021-12-19T09:47:41+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=211'
permalink: /2021/12/19/siri-python-python-skripte-starten-mit-siri/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/12/Thumbnail-fenster-siriri.jpg'
categories:
    - 'Bots und Automatisierung'
    - MacOS
tags:
    - Automatisierung
    - MacoS
    - Python
    - python3
    - Siri
---

<figure class="wp-block-image size-large">![Bild zeigt eine Berglandschaft und die Begriffe Python und Siri](https://christoph-schmalfuss.de/blog/wp-content/uploads/2021/12/Thumbnail-fenster-siriri-1024x576.jpg)</figure>Seit MacOS Monterey lassen sich auf jedem Mac eigene Siri Befehle erstellen. Damit lassen sich grundsätzlich alle möglichen Mac-Funktionen automatisieren, ich find aber besonders spannend, dass ich damit jetzt endlich all meine Python-Skripte mit Siri steuern kann. Und wie das funktioniert, schauen wir uns jetzt an.

## Skript erstellen und finden

Als erstes brauchen wir natürlich ein Skript, das wir starten können. Ich hab so ein Skript jetzt schon mal erstellt. Das Skript hat nur einen Befehl und zwar print(‚Hallo Welt!‘). Es macht also nichts anderes, als hallo zu sagen. Ihr könnt aber natürlich auch viel kompliziertere Skripte nutzen. Alles was ihr von Hand starten könnt, könnt ihr auch mit Siri starten.

Als nächstes müssen wir wissen, wo unser Skript liegt. Ich habe mein Skript einfach mein\_skript.py genannt – und den Namen kann ich einfach über das Terminal suchen. Dafür kann ich z.B. mdfind nutzen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-bash" data-lang="Bash">```
mdfind mein_skript.py

Antwort:
/Users/Chris/mein_skript.py
/Users/Chris/Library/Application Support/Sublime Text 3/Local/Auto Save Session.sublime_session
/Users/Chris/Library/Application Support/Sublime Text 3/Local/Session.sublime_session
```
```

</div>Ich krieg jetzt hier mehrere Ergebnisse zurück. Das sind teilweise so automatisch gespeicherte Sicherheitskopien, aber hier oben ist tatsächlich auch meine python-Datei. Ich kopier mir jetzt den Pfad der Datei, denn den brauchen wir gleich noch einmal.

Wir starten jetzt mal testweise unser Skript. Und ein Python Skript starten wir ja mit dem Befehl python3 und dann dem Pfad des Skripts. Entsprechend schreibe ich:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-bash" data-lang="Bash">```
python3 /Users/Chris/mein_skript.py
```
```

</div>Das funktioniert tadellos, wir können als jetzt loslegen und Siri einen neuen Befehl beibringen.

## Siri programmieren

Ich drücke als erstes Command und die Leertaste, um meine Spotlight-Suche zu starten. Und hier suche ich jetzt nach „Kurzbefehle“. Das ist das Programm, mit dem man eigene Siri-Befehle bauen kann.

Als nächstes erstelle ich einen neuen Befehl, indem ich Command und N drücke. Ganz oben lege ich jetzt den Kurzbefehl-Name fest. Das ist dann auch genau der Befehl, den ich sagen muss, damit Siri etwas für mich macht. Ich entscheide mich jetzt für was ganz einfaches aber eindeutiges, z.B. „Starte mein cooles Skript“.

Auf der rechten Seite haben wir jetzt eine Menge Aktionen, die wir theoretisch ausführen können. Ich will mich aber mal auf die Funktionen beschränken, die wir wirklich brauchen. Wir wollen ja, dass das Terminal geöffnet wird und dann ein Befehl ausgeführt wird, der das Python-Skript startet.

Und dafür schreiben wir ein kleines Apple-Skript. Dafür suche ich zuerst nach „AppleScript ausführen“. Und dann ziehe ich das Element in meinen Arbeitsbereich. Hier habe ich jetzt schon etwas Code vorgegeben. Den brauchen wir nicht und schreiben stattdessen selbst ein paar Zeilen. Ich schreibe kurz mal den Befehl auf und erkläre gleich, was passiert.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-bash" data-lang="Bash">```
tell application "Terminal" to do script "python3 /Users/Chris/mein_skript.py"

```
```

</div>## Siri antworten lassen

Ich sage also jetzt dem Programm Terminal, einen bestimmten Befehl auszuführen. Jetzt machen wir das ganze noch bisschen lebendiger. Wenn Siri nämlich den Befehl verstanden hat, soll sie uns noch kurz Bescheid geben. Dafür suche ich nach „Text sprechen“ und ziehe das Element in meinen Arbeitsbereich. Und hier kann ich jetzt einen beliebigen Text von Siri sprechen lassen. Wir können ja mal so etwas nehmen wie „Alles klar, Skript wird gestartet.“ Und hier kann ich jetzt noch die Stimme auswählen, da nehm ich gern Helena.

Wir können auch gleich mal testen, ob das funktioniert. Dazu klicke ich oben rechts auf „Ausführen“.

Das sieht gut aus, das funktioniert also schon mal theoretisch. Jetzt wollen wir aber natürlich testen, ob das auch in der freien Wildbahn funktioniert. Deshalb mach ich jetzt mal alles zu und wir schauen mal, ob Siri reagiert.

„*Hey Siri, Starte mein cooles Skript*.“

Und wie ihr seht funktioniert das wunderbar – und damit haben wir es für heute geschafft. Das ganze Thema Mac-Automation ist übrigens suuuper spannend, ich kann euch nur empfehlen, einfach damit mal ein wenig rumzuspielen. Wenn das Video hier bei euch gut ankommt, werde ich bestimmt auch noch das ein oder andere Video zu diesem Thema machen. Jetzt wünsch ich euch aber erstmal eine wunderschöne Woche, bleibt neugierig und bis bald!