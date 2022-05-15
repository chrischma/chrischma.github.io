---
id: 381
title: 'Python if __name__ == &#8222;__main__&#8220; einfach erklärt! | Python Tutorial für Anfänger (Deutsch)'
date: '2022-04-30T10:08:57+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=381'
permalink: /2022/04/30/python-if-__name__-__main__-einfach-erklaert-python-tutorial-fuer-anfaenger-deutsch/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Thumbnail-name.png'
categories:
    - 'Kurze Tipps'
tags:
    - Python
---

Heute soll es um eine berühmt berüchtigte Codezeile gehen, die ihr garantiert schon einmal in einem Python Skript gesehen habt. Und zwar ist das die Zeile „if \_\_name\_\_ == „\_\_main\_\_“. Was die macht und wie die funktioniert erkläre ich euch jetzt. Viel Spaß!

<figure class="wp-block-image size-large">![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Thumbnail-name-1024x576.png)</figure>## Wofür brauche ich name == main?

Fangen wir vielleicht erstmal damit an zu verstehen, warum diese Zeile so ziemlich in jedem komplexeren Python Skript auftaucht. **Kurz gesagt: `if name == "main" ` wird verwendet, um zu prüfen, ob ein Skript gerade direkt aufgerufen wird.** Und wenn das Skript direkt aufgerufen wird, dann wird eine bestimmte Funktion ausgeführt. Am einfachsten kann man das verstehen, wenn wir uns das Skript hier angucken.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def main():
	print('Hello World')


if __name__ == "__main__":
    main()
```
```

</div>Das Skript besteht nur aus einer Funktion. Die wird ganz oben definiert und heißt einfach main(). Und was die main-Funktion dann macht, das kann natürlich sehr unterschiedlich sein. In unserem Fall macht die Funktion einfach eine Ausgabe „Hello World“.

Und mit `if name == "main" ` lege ich jetzt also fest: Wenn mein Skript direkt aufgerufen wird, rufe bitte die Funktion main() auf, also die Funktion, die Hello World ausgibt.

(Ausprobieren)

Das funktioniert schon mal ganz gut, die Frage ist jetzt aber natürlich, warum ich den ganzen Bumms überhaupt brauche. Dann theoretisch könnte ich mein Skript ja auch komplett ohne `if name == "main" ` gestalten.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def main():
	print('Hello World')


main()
```
```

</div>Das ist auch an sich nicht ganz falsch, wir müssen aber beachten, dass es natürlich auch andere Arten und weisen gibt, ein Skript aufzurufen.

Ich hab hier mal ein zweites Skript angelegt. Und wir nehmen jetzt mal an, dass ich Funktionen aus meinem ersten Skript im zweiten Skript verwenden möchte. Dafür könnten wir ja das erstes Skript einfach importieren und dann auf die Funktionen aus dem ersten Skript zugreifen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import mein_skript
```
```

</div>Blöd ist nur: Jetzt wird die Funktion, die Hello World ausgibt, sofort beim import aufgerufen. Meistens wollen wir das aber gar nicht, sondern wir wollen die Funktionen aus dem anderen Skript einmal importieren aber erst dann aufrufen, wenn wir sie wirklich brauchen. Und da kommt jetzt wieder`if name == "main" `Skript aufrufen, passiert etwas ziemlich interessantes: Die Funktion Main, die Hello World ausgibt, wird jetzt nicht mehr aufgerufen, weil Python erkannt hat „Okay, hier wird gerade nur ein Skript importiert und nicht direkt ausgeführt, da feuere ich die Hello World jetzt noch nicht ab, sondern erst, wenn sie aufgerufen wird.“ Und das ist einfach eine sehr praktische Unterscheidung, die wir gerade bei größeren Projekten immer wieder brauchen, wenn sich unser Skript auf mehrere Skripte und Module aufteilt.

## Was ist \_\_name\_\_?

Klar ist jetzt schon mal, wofür die Codezeile verwendet wird. Bleibt nur noch die Frage, wie das ganze eigentlich funktioniert. Dafür schauen wir uns am besten mal die Bestandteile im einzelnen an.`if` ist erstmal klar. Damit können wir prüfen, ob eine Bedingung erfüllt ist. `__name__` ist da schon etwas interessanter. Das Teil nennt sich Dunder Name, und der Name kommt einfach durch die beiden doppelten Unterstriche zu Stande, also die beiden Double Underscores oder Kurs Dunderscores. `__name__` ist eine besondere Variable. Und die hat die Eigenschaft, dass sie immer den Wert `__main__` trägt, wenn das Skript gerade direkt aufgerufen wird. Das können wir ziemlich einfach testen, indem wir uns die Variable ausgeben lassen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def main():
	print('Hello World')

print(__name__)

if __name__ == "__main__":
    main()

# >>> Das Skript gibt zurück: "__main__"
```
```

</div>Anders sieht das aus, wenn wir uns anschauen, welchen Wert die Variable `__name__` hat, wenn wir unser Skript über ein anderes Skript importieren.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import mein_skript

print(mein_skript.__name__)

# >>> Das Skript gibt zurück: mein_skript
```
```

</div>Und damit ist die Unterscheidung eigentlich schon klar. Wir gucken mit `if name == "main" ` also als erstes nach dem Wert der Variable `__name__`. Und der ist immer `__main__`, wenn das Skript direkt aufgerufen wird. Und wenn dieser Wert gleich `__main__` ist und nicht einen anderen Wert hat, dann soll `main()` ausgeführt werden. Und somit wir jetzt also Hello World immer nur dann aufgerufen, wenn wir das Skript direkt aufrufen. Und wenn wir das Skript nur importieren, passiert nichts.

Und das ist eigentlich auch schon die ganze Magie hinter dem Mythos \_\_name\_\_ == \_\_main\_\_.