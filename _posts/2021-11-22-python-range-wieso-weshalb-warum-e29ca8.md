---
id: 191
title: 'Python range – Wieso, weshalb, warum ✨'
date: '2021-11-22T18:00:19+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=191'
permalink: /2021/11/22/python-range-wieso-weshalb-warum-%e2%9c%a8/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/11/Thumbnail-fenster-range.jpg'
categories:
    - Effizienz
tags:
    - Python
---

<figure class="wp-block-image size-large">![Ein Computerfenster mit zwei Schriftzügen: Python und Range](https://christoph-schmalfuss.de/blog/wp-content/uploads/2021/11/Thumbnail-fenster-range-1024x576.jpg)</figure>Heute geht es um die range Funktion in Python. Die gehört zu den Funktionen, die standardmäßig in Python enthalten sind und die wir auch immer wieder brauchen werden. Grundsätzlich kann man die Funktion verwendet, um Zahlenfolgen zu erzeugen. Man kann mit ihr aber auch ziemlich praktische Schleifen basteln.

So eine range-Zahlenfolge beginnt normalerweise bei Null und endet, sobald eine bestimmte Zahl erreicht ist. Wenn ich also range(6) aufrufe, bekomme ich z.B. eine Zahlenfolge zurück, die von 0 zählt, bis sie bei 6 ankommt:

0, 1, 2, 3, 4, 5

Ganz wichtig zu beachten: Die Zahl, die ich in der Klammer angebe, ist selbst nicht in der range enthalten, die wir zurückbekommen. Die Zahl ist sozusagen die Stop-Zahl, die nicht mehr in unserer Range aufzaucht. Und genau deshalb endet unsere range(6) hier bei der Zahl 5.

Die Funktion kann aber natürlich noch viel mehr. Und das schauen wir uns am besten mal direkt im Quellcode an.

## Parameter der range()-Funktion

Wie ihr gerade schon gesehen habt, ist es ziemlich einfach, die range-Funktion zu nutzen. Ich kann z.B. eine Variable anlegen mit dem Namen r. In dieser Variable rufe ich die range-Funktion auf und lasse mir das Ergebnis anzeigen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
r = range(6)
print(r)

# Antwort: range(0,6)
```
```

</div>Als Ergebnis erhalte ich jetzt ein range-Objekt von 0 bis 6. Vielleicht wundert ihr euch jetzt, warum wir einfach nur so ein range-Objekt zurückbekommen, obwohl wir eigentlich erwartet hätten, dass jetzt alle Zahlen von 0 bis 5 aufgelistet werden. Das liegt einfach an der Art und Weise, wie die Funktion arbeitet. Das können wir aber glücklicherweise ändern, indem wir uns unsere Range als Liste anzeigen lassen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
r = range(6)
print(list(r))

# Antwort: [0, 1, 2, 3, 4, 5]
```
```

</div>Ich kann aber genauso gut mit range() Zahlenfolgen erstellen, die nicht wie bisher bei 0 beginnen. Dazu kann ich vor meiner gewünschten Stop-Zahl noch eine Start-Zahl angeben. Die muss ich beim Aufrufen meiner range-Funktion einfach als erstes in die Klammer schreiben.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
r = range(2, 6)
print(list(r))

# Antwort: [2, 3, 4, 5]

```
```

</div>Witzigerweise gibt es jetzt aber noch eine dritte Zahl, die wir angeben können. Mit der können wir bestimmen, wie groß die Schritte zwischen den Zahlen sind. Normalerweise zählt die range-Funktion ja immer in 1er-Schritten, ich kann aber z.B. auch in 2er-Schritten zählen lassen. So kann ich mir z.B. alle geraden Zahlen zwischen 0 und 99 anzeigen lassen:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
r = range(0, 99, 2)
print(list(r))

# Antwort: [0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 50, 52, 54, 56, 58, 60, 62, 64, 66, 68, 70, 72, 74, 76, 78, 80, 82, 84, 86, 88, 90, 92, 94, 96, 98]
```
```

</div>Das sind alles nette Spielereien, aber am spannendsten ist, was man mit der Funktion in der Praxis macht. Neben dem Erzeugen von Zahlenfolgen ist die Funktion super beliebt, um damit Schleifen zu basteln. Nehmen wir z.B. an, wir wollen 10x „Moin“ in unserer Konsole anzeigen. Dafür können wir die range Funktion mit der for-Schleife kombinieren.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
for i in range(10):
    print('Moin!')

# Antwort:
Moin!
Moin!
Moin!
Moin!
Moin!
Moin!
Moin!
Moin!
Moin!
Moin!
```
```

</div>Python geht jetzt hier einfach durch alle Zahlen unserer range durch und führt für jede Zahl in dieser einmal den print-Befehl aus. Unsere range enthält ja 10 Zahlen, und deshalb wird der Befehl auch 10x ausgeführt. Und das ist tatsächlich eine sehr bequeme und kurze Methode, um bestimmte Vorgänge mit einer bestimmten Anzahl von Wiederholungen durchzuführen.

Ok, soviel erstmal zum Thema range-Funktion.