---
id: 320
title: 'Die Selenium Extension, die Python Code von selbst schreibt'
date: '2022-04-09T07:44:09+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=320'
permalink: /2022/04/09/die-selenium-extension-die-python-code-von-selbst-schreibt/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Thumbnail-Selinium-Automoatschi.jpg'
categories:
    - 'Bots und Automatisierung'
    - Selenium
---

Hallo und herzlich willkommen zurück. Heute möchte ich euch eine Browser-Extension vorstellen, die uns beim Automatisieren mit Python ganz schön viel Arbeit abnehmen kann. Mit ihr können wir z.B. bequem Elemente suchen oder uns direkt echten Python Code ausgeben lassen. Schauen wir uns mal an, wie das ganze funktioniert.

<figure class="wp-block-embed is-type-video is-provider-youtube wp-block-embed-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" frameborder="0" height="387" loading="lazy" src="https://www.youtube.com/embed/a0xmZVt1DoE?feature=oembed" title="Eine Browser-Erweiterung, die Python Code von selbst schreibt! ✨ | Automatisierung Tutorial Deutsch" width="688"></iframe></div></figure>## Selenium IDE installieren (Chrome)

Um die Erweiterung zu installieren öffnen wir einfach den folgenden Link, den ich euch natürlich wie immer auch in die Kommentarspalte schreibe:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
https://chrome.google.com/webstore/detail/selenium-ide/
```
```

</div>Und dort klicken wir dann auf „Hinzufügen“ und bestätigen das. Anschließen legen wir uns die Erweiterung noch auf den Schnellzugriff, indem wir oben rechts auf das Puzzelteil klicken und dann auf das Pin-Symbol. Selenium IDE ist jetzt installiert und wir können direkt loslegen.

<figure class="wp-block-image size-large">![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Bildschirmfoto-2022-04-09-um-09.13.40-1024x739.png)</figure>## Einfaches Beispiel

Als kleines Beispiel wollen wir jetzt ein Skript erstellen, dass uns das Wetter am Garadasee für die nächsten 16 Tage anzeigt. Dafür starten wir die Extension, vergeben einen Namen und legen die Start-URL fest, auf der wir beginnen wollen.

Und danach können wir auch schon auf das Aufnahmesymbol klicken. Die Erweiterung beginnt dann, alles was wir machen, also Klicks, Tastatureingaben usw. aufzuzeichnen. Und wenn ich fertig bin, klick ich hier einfach auf Stop.

Bestenfalls sollte ich jetzt prüfen, ob auch alles sauber erfasst wurde und mein Skript so erstmal funktioniert. Und dafür klicke ich hier auf Play. Selenium spielt jetzt meine Befehle erneut ab.

## Elemente untersuchen

<figure class="wp-block-image size-large">![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Bildschirmfoto-2022-04-09-um-09.27.28-1024x615.png)</figure>So weit so klar, spannend ist aber vor allem, was Selenium uns hier für Informationen speichert. Wir können uns hier nämlich für jeden ausgeführten Befehl alle Details anzeigen lassen. Hier z.B. kann ich sehen, dass auf einen Link mit einem bestimmten Text geklickt wurde. Für den Link selbst kann ich mir jetzt noch andere Identifikationsmerkmale anschauen, also z.B. die CSS Bezeichnung oder den XPATH. Und das sind ja zwei Informationen, die wir so super in unsere Python Skripte kopieren können, wenn wir einzelne Elemente identifizieren wollen.

Genauso schön kann ich hier aber auch z.B. Tastatureingaben nachvollziehen. Und das ist schon echt praktisch, um schneller eine Automatisierung mit Python basteln zu können, die genau das tut, was man will.

## Automatisch generierten Python Code ausgeben lassen

Wir wollen das ganze jetzt mal noch auf die Spitze treiben. Statt überhaupt noch selbst etwas zu programmieren, können wir uns unsere Befehle nämlich direkt als fertigen Python Code ausgaben lassen. Dafür mache ich eine Rechtsklick auf mein Projekt und klicke auf Export. Hier kann ich jetzt Python auswählen und klicke dann auf Export.

Meiner Datei gebe ich jetzt einen passenden Namen, also z.B. Selenium Wetter, speichere das ganze und schon habe ich ein fertiges Python Skript, das alle Schritte ausführt, die ich vorher aufgenommen habe.

<figure class="wp-block-image size-large">![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Bildschirmfoto-2022-04-09-um-09.43.05-1024x781.png)<figcaption>So sieht der Code aus, der direkt von Selenium ausgespuckt wird.</figcaption></figure>## Fazit

Natürlich ist dieser automatische Code bei weitem nicht perfekt. Ich finde z.B., dass er – gerade weil er nicht natürlich gegliedert ist – nicht so toll zu lesen ist. Außerdem müssen wir natürlich alle Variablen noch einbauen, die wir verwenden wollen. Wenn wir also z.B. eine lange Liste an Städten haben, für die wir das Wetter raussuchen wollen, dann müssen wir die entsprechenden Variablen immer noch definieren und an den richtigen Stellen im Skript einfügen.

Außerdem bleibt uns das Debuggen natürlich nicht erspart. Ohne eine Überarbeitung und ohne dass wir nochmal über mögliche Fehlerquellen nachdenken, läuft so ein Skript selten richtig zuverlässig.

Dennoch kann so ein Skript wirklich eine sehr bequem erstellte Arbeitsgrundlage sein, die uns zumindest den dümmsten Teil der Arbeit des Automatisierens abnimmt, nämlich z.B. das mühsame Suchen nach einzelnen Elementen. Und schon allein deshalb lohnt es sich, einfach mal ein bisschen mit der Extension herumzuspielen.

Aber natürlich ist selbstgemacht ja doch irgendwie immer am schönsten – und das gilt für das Schreiben von Quellcode ganz offensichtlich also auch.

 Und damit sind wir auch schon am Ende angelangt. Ganz herzlichen Dank fürs Zuschauen, bleibt neugierig und bis nächste Woche!