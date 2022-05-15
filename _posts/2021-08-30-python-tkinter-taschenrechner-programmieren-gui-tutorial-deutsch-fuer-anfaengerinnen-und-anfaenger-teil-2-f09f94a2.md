---
id: 38
title: 'Python tkinter | Taschenrechner programmieren | GUI Tutorial (Deutsch) | für Anfängerinnen und Anfänger | Teil 2 🔢'
date: '2021-08-30T07:21:18+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=38'
permalink: /2021/08/30/python-tkinter-taschenrechner-programmieren-gui-tutorial-deutsch-fuer-anfaengerinnen-und-anfaenger-teil-2-%f0%9f%94%a2/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/08/Thumbnail-taschenrechner.png'
categories:
    - 'GUI (Graphical User Interface)'
---

[Im ersten Tutorial](https://christoph-schmalfuss.de/blog/?p=28) haben wir bereits ein hübsches Userinterface erzeugt. Und heute bringen wir dem Taschenrechner endlich wirklich bei, zu rechnen.

Grundsätzlich wird der Rechner so funktionieren, dass wir eine Zeichenkette festlegen, die aus all den Buttons besteht, die gedrückt wurden. Am Anfang wird die Zeichenkette leer sein. Wenn der Nutzer dann z.B. die 5 auf dem Userinterface drückt, wird die 5 zu dieser Zeichenkette hinzugefügt. Wenn der Nutzer + drückt, wird entsprechend ein + hinzugefügt usw. Das = bekommt bei uns eine besondere Bedeutung. Wenn das gedrückt wird, schnappt sich Python die eingegebene Zeichenkette und berechnet sie.

Und noch eine Taste bekommt eine Sonderrolle, nämlich AC. Mit der Taste wird die Zeichenkette geleert, und eine neue Berechnung kann beginnen.

Als erstes brauchen wir also eine leere Zeichenkette.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
calculation = str()
```
```

</div>Als nächstes basteln wir uns eine Funktion, die den Wert des Buttons an die Zeichenkette weitergibt.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def add_button_text_to_calculation(value):
    global calculation

    calculation = calculation + value
    output_label['text'] = calculation
```
```

</div>Für die Buttons AC und = müssen wir noch ein paar Sonderfälle einbauen. Wenn der Button AC gedrückt wird, soll die Berechnung abgebrochen werden. Und wenn das **=** gedrückt wird, soll die Zeichenkette berechnet werden.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def add_button_text_to_calculation(value):
    global calculation

    # AC (also known as 'ALL CLEAR') will clear the current calculation.
    if value == 'AC':
        calculation = str()
        output_label['text'] = '...'
        return

    if value == '=':
        calculate(calculation)
        calculation = str()
        return

    calculation = calculation + value
    output_label['text'] = calculation
```
```

</div>Jetzt schreiben wir die Funktion, die aus der Zeichenkette eine Berechnung macht – und das Ergebnis berechnet. Dafür nutzen wir die eval Funktion. Sorgt dafür, dass Python eine Zeichenkette nicht einfach als eine Reihe von zusammengewürfelten Zeichen versteht, sondern das Python diese Zeichen so behandelt, als wären es echte Python Befehle.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def calculate(calc):
    try:
        result = eval(calc)
        print(result)
        output_label['text'] = result

```
```

</div>Wichtig an der Stelle: Wenn der User irgendwelchen Quatsch eingetippt hat, dann soll unser Taschenrechner nicht abstürzen, sondern einen Fehler zurückgeben. Dafür schreiben wir eine Exception, also eine Ausnahme.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```

    except Exception as e:
        print(e)
        output_label['text'] = 'Error'
```
```

</div>In einem letzten Schritt müssen die Buttons erfahren, was sie eigentlich tun sollen. Und deshalb bringen wir ihnen jetzt bei, ihren Wert in die Zeichenkette zu übergeben. Die entsprechende Funktion haben wir ja schon geschrieben, das war „add\_button\_text\_to\_calculation“. Wir verknüpfen jetzt also alle Buttons mit dieser Funktion. Dafür legen wir einfach ein Command, also einen Befehl fest.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def create_button(value):
    button = tkinter.Button(text=value, command=lambda: add_button_text_to_calculation(value))
    gui_items.append(button)
```
```

</div>Falls ihr euch über den Begriff lambda wundert – mit diesem erzeugen wir eine anonyme Funktion. Anonym heißt diese Funktion, weil sie selbst keinen Namen trägt, sondern stattdessen den Platzhalternamen lambda hat. Das ist nochmal ein ganz eigenes Thema, und deshalb verlinke ich euch in der Videobeschreibung ein Tutorial, das darauf nochmal genauer eingeht.

Was aber trotzdem wichtig ist, ist die Frage, warum wir hier überhaupt eine neue lambda-Funktion definieren müssen, obwohl wir ja eigentlich schon eine Funktion haben, nämlich add\_button\_text\_to\_calculation. Der Grund dafür ist, dass wir ja wollen, dass die Funktion erst dann aufgerufen wird, wenn der Button gedrückt wird – und nicht schon dann, wenn Python zum ersten Mal den Code interpretiert. Würde ich lambda jetzt weglassen, würde genau das passierten. Python würde bei interpretieren des Codes die Funktion auslösen, ohne dass ich den Button gedrückt hab.

Wenn lambda allerdings dabei ist ist, dann ist das hier keine Zeile mehr, in der eine Funktion aufgerufen wird, sondern es ist eben eine Zeile, in der eine Funktion definiert wird. Und wie wir wissen, werden Funktionen beim Definieren noch nicht aufgerufen, sondern erst dann, wenn wir es wollen. Somit kann Python diesen Code interpretieren, ohne dass die Funktion aufgerufen wird. Und wenn wir den Button klicken, wird die Funktion dann tatsächlich aufgerufen.

Und damit haben wir es geschafft.

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


def add_button_text_to_calculation(value):
    global calculation

    # AC (also known as 'ALL CLEAR') will clear the current calculation.
    if value == 'AC':
        calculation = str()
        output_label['text'] = '...'
        return

    if value == '=':
        calculate(calculation)
        calculation = str()
        return

    calculation = calculation + value
    output_label['text'] = calculation


def calculate(calc):
    try:
        result = eval(calc)
        print(result)
        output_label['text'] = result

    except Exception as e:
        print(e)
        output_label['text'] = 'Error'


def create_button(value):
    button = tkinter.Button(text=value, command=lambda: add_button_text_to_calculation(value))
    gui_items.append(button)


for val in button_values:
    create_button(val)


output_label = tkinter.Label(text='Hallo.')
output_label.grid(row=0, columnspan=10)

# All buttons will be auto-placed in a grid
# with maximum 3 columns and endless rows here:
column_count = 0
row_count = 1
maximum_columns = 3

for item in gui_items:
    item.grid(row=row_count, column=column_count)

    column_count += 1
    if column_count == maximum_columns:
        column_count = 0
        row_count += 1


if __name__ == '__main__':
    window.mainloop()

```
```

</div>