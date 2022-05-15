---
id: 169
title: 'Python Tkinter: Eingabe lesen'
date: '2021-11-19T13:53:13+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=169'
permalink: /2021/11/19/python-tkinter-eingabe-lesen/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/11/Thumbnail-fenster-eingabe.jpg'
categories:
    - Uncategorized
---

<figure class="wp-block-image size-large">![Ein Computerfenster, das die Wörter Python und Eingabefeld enthält.](https://christoph-schmalfuss.de/blog/wp-content/uploads/2021/11/Thumbnail-fenster-eingabe-1024x576.jpg)</figure>Heute schauen wir uns an, wie man mit Python ein Eingabefeld erstellen und auslesen kann.

Wir benutzen für unser Programm das Modul tkinter, mit dem man ziemlich einfach grafische Oberflächen erzeugen kann. Das Modul ist schon vorinstalliert, wir müssen also nichts weiter installieren, sondern müssen das Modul nur in unser Skript importieren.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from tkinter import *
```
```

</div>Als nächstes erzeugen wir ein Fenster und geben dem Fenster auch gleich mal einen Namen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
window = Tk()
window.title("Eingabe")
```
```

</div>In unserem Fenster wollen wir jetzt zwei Elemente haben. Einmal ein Eingabefeld und dann noch einen kleinen Button, mit dem wir die Eingabe bestätigen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
input_field = Entry(window)
ok_button = Button(text='Ok')
```
```

</div>Beide Felder existieren jetzt schon mal, wir müssen sie aber noch auf unserem Fenster platzieren.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
input_field.pack()
ok_button.pack()

```
```

</div>Jetzt müssen wir eigentlich Tkinter nur noch einen Startbefehl geben.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
window.mainloop()
```
```

</div>Probieren wir aus, was passiert!

<figure class="wp-block-image size-large">![Screenshot eines Computerfensters mit einem Eingabefeld und einem "OK"-Button](https://christoph-schmalfuss.de/blog/wp-content/uploads/2021/11/Bildschirmfoto-2021-11-19-um-14.37.56-1024x676.png)</figure>Das Fenster wird jetzt schon mal angezeigt. Blöderweise macht unser Button aber noch nichts. Kann er aber auch nicht, denn wir haben ja noch nicht festgelegt, was er überhaupt machen soll. Wir wollen ja den Text aus dem input\_field lesen und dafür schreiben wir jetzt die entsprechende Funktion.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def read_input_field():
    current_input = input_field.get()
    print(current_input)

```
```

</div>Jetzt müssen wir die Funktion nur noch mit dem Button verknüpfen. Das funktioniert über den Command-Parameter, den wir einfach dort festlegen, wo wir unseren Button erstellt haben.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
ok_button = Button(text='Ok', command=read_input_field)
```
```

</div>Probieren wir es aus!

Und schon haben wir es geschafft.

## ✅ Kompletter Quellcode

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from tkinter import *


def read_input_field():
    current_input = input_field.get()
    print(current_input)


window = Tk()
window.title("Eingabe")

input_field = Entry(window)
ok_button = Button(text='Ok', command=read_input_field)

input_field.pack()
ok_button.pack()

window.mainloop()

```
```

</div>