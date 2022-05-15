---
id: 220
title: 'Python Skript im Hintergrund weiterlaufen lassen (Linux, MacOS) | nohup'
date: '2022-01-04T08:07:13+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=220'
permalink: /2022/01/04/python-skript-im-hintergrund-weiterlaufen-lassen-nohup-linux-macos/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2022/01/thumbnail-nohup.jpg'
categories:
    - Linux
    - MacOS
    - 'MacOS und Linux'
---

<figure class="wp-block-embed is-type-video is-provider-youtube wp-block-embed-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" frameborder="0" height="387" loading="lazy" src="https://www.youtube.com/embed/Cw3eW4mrqY0?feature=oembed" title="Python Skript im Hintergrund laufen / weiterlaufen lassen 🕶️ (Linux, MacOS) | mit nohup" width="688"></iframe></div></figure>Wenn wir ein Python Skript z.B. über das Terminal starten, dann läuft das Skript immer nur so lange, bis wir das Terminal-Fenster schließen. Ich habe hier z.B. ein kleines Python Skript geschrieben, das mir permanent zufällige Zahlen anzeigt. Und das Skript läuft auch so erstmal ganz gut. Wenn ich das Skript starte, dann könnt ihr hier oben sehen, wie ständig neue Zahlen hereinflattern. Wenn ich allerdings jetzt mein Terminal schließe, dann läuft mein Programm nicht weiter.

Glücklicherweise gibt es aber einen praktischen Befehl, der uns genau für dieses Problem die Lösung bietet. Und der heißt nohup. Der wird normalerweise dafür verwendet, um Prozesse auf Servern weiterlaufen zu lassen, auch wenn z.B. die Verbindung zum Server abbricht. Aber er löst eben auch unser kleines Python Problem.

Ich muss dafür nur eine Sache machen. Ich starte mein Skript ja normalerweise mit dem Befehl python3 meinskript.py. Und vor diesen Befehl schreibe ich jetzt einfach das Wörtchen nohup.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-bash" data-lang="Bash">```
nohup python3 mein_skript.py
```
```

</div>Wie ihr seht läuft mein Programm jetzt wieder. Und wenn ich jetzt mein Fenster schließe, dann läuft das Programm ebenfalls weiter. Und damit haben wir eigentlich schon die Lösung gefunden.

Blöd ist nur, dass das Programm jetzt erstmal ewig im Hintergrund weiterlaufen würde. Aber es gibt natürlich einen Befehl, wie wir unser Programm trotzdem noch beenden können. Dazu lassen wir uns zunächst einmal die Prozesse auflisten, die gerade über unserem Benutzer laufen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-bash" data-lang="Bash">```
ps -U Chris | grep mein_skript.py
```
```

</div>Und um jetzt meinen Prozess zu beenden, nutzen wir den Befehl kill.

Der besteht in seiner einfachsten Form aus zwei Teilen, nämlich dem Wort kill und der ID des Prozesses, den wir beenden wollen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-bash" data-lang="Bash">```
kill 11486
```
```

</div>Ja und so einfach kann man also Prozesse wie Python-Skripte im Hintergrund weiterlaufen lassen. Und damit haben wir es für heute geschafft.