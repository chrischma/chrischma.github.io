---
id: 28
title: 'Python tkinter | Taschenrechner programmieren | GUI Tutorial (Deutsch) | für Anfängerinnen und Anfänger 🔢'
date: '2021-08-17T07:23:52+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=28'
permalink: /2021/08/17/python-tkinter-taschenrechner-programmieren-gui-tutorial-deutsch-fuer-anfaengerinnen-und-anfaenger-%f0%9f%94%a2/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/08/Thumbnail-taschenrechner.png'
categories:
    - 'GUI (Graphical User Interface)'
---

<figure class="wp-block-image size-large">![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2021/08/taschenrechner-1024x385.png)</figure>Wir programmieren einen Taschenrechner. Los geht’s!

Das hier ist das erste von zwei Tutorials. Heute werden wir das Userinterface erstellen und beim nächsten Mal werden wir dann die Funktionen schreiben, die die eigentliche Berechnung machen.

Für das Userinterface nutzen wir das Modul tkinter. Das ist bereits vorinstalliert, wir können es also direkt importieren.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import tkinter
```
```

</div>Danach legen wir uns ein neues Fenster an und legen einige Eigenschaften fest.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
window = tkinter.Tk()
window.geometry('150x220')
window.title('Rechner')
window.mainloop()
```
```

</div>Und jetzt können wir auch schon all die Buttons vorbereiten, die wir später brauchen werden. Dafür schreibe ich alle Buttons zunächst in eine einfache Liste.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
button_values = ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0',
                 '+', '-', '*', '/', '=', 'AC']
```
```

</div>Aus diesen Elementen werden später die konkreten Userinterface-Elemente gebaut. Und um die später dann zu sammeln, lege ich schon mal eine leere Liste an.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
gui_items = list()
```
```

</div>Python weiß im Moment noch nicht, wie es aus unseren Button Values tatsächliche Buttons erstellen soll. Wir schreiben jetzt eine Funktion, die aus jedem der Elemente in unserer Liste einen Button erstellt und diesen Button in die Liste unserer GUI-Items ablegt.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def create_button(value):
    button = tkinter.Button(text=value)
    gui_items.append(button)
```
```

</div>Die Funktion ist erstellt – und jetzt führen die Funktionen für alle Elemente unserer Liste aus:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
for val in button_values:
    create_button(val)
```
```

</div>Neben vielen hübschen Buttons braucht unser Taschenrechner auch eine Anzeige, wo z.B. das Ergebnis einer Rechnung angezeigt werden kann. Dafür erstellen wir ein Label.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
output_label = tkinter.Label(text='Hallo.')
output_label.grid(row=0, columnspan=10)
```
```

</div>All die vielen Buttons, die wir erstellt haben, müssen jetzt noch in der richtigen Art und Weise in unserem Fenster angeordnet werden. Und dafür machen wir jetzt tatsächlich mal ein wenig Python-Magie. Unsere Buttons sollen für unseren Taschenrechner in drei Spalten angeordnet werden. Denn das ist für den Nutzer dann natürlich deutlich angenehmer zu bedienen, als wenn alle Buttons einfach in einer Reihe dargestellt werden würden.

Wir bringen Python jetzt dazu, durch die Elemente durchzugehen und immer auf eine neue Zeile zu springen, wenn sich schon drei Elemente in einer Zeile befinden.

Als erstes legen wir Variablen fest, mit denen Python dann zählen wird.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
column_count = 0
row_count = 1
max_columns = 3
```
```

</div>Python soll jetzt durch die Liste der GUI-Elemente gehen und die Elemente im Gitter ausrichten.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
for item in gui_items:
    item.grid(row=row_count, column=column_count)

    column_count += 1
```
```

</div>Jetzt bauen wir noch einen kleinen Kniff ein. Wenn Python nämlich in der dritten Spalte angekommen ist, soll Python eine Zeile nach unten springen und wieder bei der ersten Spalte weitermachen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
    if column_count == max_columns:
        column_count = 0
        row_count += 1
```
```

</div>Das Interface ist soweit fertig und wir können das ganze ausführen. Ich schreibe dafür abschließend noch die Name = Main Funktion. Die habt ihr bestimmt schon einmal in anderen Videos oder Quellcodes gesehen. Die macht eigentlich nur eine Sache: Sie schaut, ob das Skript gerade direkt aufgerufen oder nur importiert wird. Wenn es aufgerufen wird, führt das Skript eine bestimmte Funktion aus. In unserem Fall soll die Mainloop gestartet werden, sobald das Skript direkt ausgeführt wird.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
if __name__ == '__main__':
    window.mainloop()
```
```

</div>Und damit haben wir es geschafft. Weiter geht es mit dem zweiten und letzten Teil, wo wir dem Taschenrechner beibringen, wirklich zu rechnen.

## ✅ Kompletter Quellcode

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import tkinter

window = tkinter.Tk()
window.geometry('150x220')
window.title('Rechner')

gui_items = list()
button_values = ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0',
                 '+', '-', '*', '/', '=', 'AC']

calculation = str()


def create_button(value):
    button = tkinter.Button(text=value)
    gui_items.append(button)


for val in button_values:
    create_button(val)

output_label = tkinter.Label(text='Hallo.')
output_label.grid(row=0, columnspan=10)

column_count = 0
row_count = 1
max_columns = 3

for item in gui_items:
    item.grid(row=row_count, column=column_count)

    column_count += 1
    if column_count == max_columns:
        column_count = 0
        row_count += 1

if __name__ == '__main__':
    window.mainloop()
```
```

</div>