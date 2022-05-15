---
id: 63
title: 'Python Tkinter | ☎️ Telefonbuch Tutorial (Deutsch)'
date: '2021-09-18T07:40:16+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=63'
permalink: /2021/09/18/python-tkinter-%e2%98%8e%ef%b8%8f-telefonbuch-tutorial-deutsch/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/09/Thumbnail-Telefonbuch.jpg'
categories:
    - 'GUI (Graphical User Interface)'
---

Hallo zurück. Heute schreiben wir ein kleines Python-Telefonbuch.

Zuerst importieren wir uns wie immer die benötigten Module. Wir nutzen heute tkinter.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import tkinter as tk
```
```

</div>Unser Telefonbuch besteht aus zwei Listen, die wir später an unterschiedlichen Stellen im Programm anzeigen. Einer Liste enthält alle Namen und eine Liste enthält alle Nummern.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
contact_names = list()
contact_numbers = list()
```
```

</div>Die Listen füllen wir dann natürlich nicht von Hand mit Daten, sondern Python soll für uns die Daten aus einer Datei auslesen. Deshalb erzeuge ich eine neue Text-Datei. Die nenne ich contacts.txt und hinterlege in ihr meine Kontakte.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
Oma Hans, 8482890
Elfride, 01473-3424021
Dieter Bohlen, +43 676 38140354
```
```

</div>Python soll jetzt diese Datei öffnen, die Daten auslesen und für uns in die Listen hinterlegen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def read_contacts_from_file():
    with open ('contacts.txt','r') as f:
        contact_strings = f.readlines()

    for contact in contact_strings:
        contact = contact.rstrip('\n')
        contact = contact.split(', ')

        contact_names.append(contact[0])
        contact_numbers.append(contact[1])


read_contacts_from_file()

```
```

</div>Jetzt wird es Zeit, unser Fenster zu erstellen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
window = tk.Tk()
window.title('Mein Telefonbuch')
window.geometry('300x300')
window.config(bg="lightblue")

numbers_label = tk.Label(text='Hallo!')
numbers_label.config(font=("Arial", 20, "bold"), bg="lightblue")

# This is where the contact_names_var will be added later

numbers_label.pack(pady=10)
contact_listbox.pack()

window.mainloop()
```
```

</div>Wir wollen alle Kontakte aus unserer Liste später in einer Listbox anzeigen. Blöderweise kann Tkinter Listen nicht direkt lesen. Aber es gibt es ein Tkinter Objekt, dass uns diese Möglichkeit eröffnet, und zwar das StringVar-Objekt. Damit wandeln wir eine Liste so um, dass sie für Tkinter lesbar ist.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
contact_names_var = tk.StringVar(value=contact_names)
contact_listbox = tk.Listbox(window, height=10, listvariable=contact_names_var)
```
```

</div>Das funktioniert jetzt schon ganz gut, allerdings ist unser Telefonbuch noch nicht interaktiv. Und darum kümmern wir uns jetzt. Wir sorgen jetzt dafür, dass Python darauf wartet, dass ein Kontakt ausgewählt wird. Und wenn ein Kontakt gewählt wurde, wird die entsprechende Telefonnummer angezeigt. Und dafür binden wir eine Funktion an die Listbox, die genau das macht.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
contact_listbox.bind('<<ListboxSelect>>', lambda e: display_number_for_contact())
```
```

</div>Die Funktion display\_number\_for\_contact schreiben wir jetzt.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def display_number_for_contact():
    i = contact_listbox.curselection()[0]
    number = contact_numbers[i]
    numbers_label['text'] = number
```
```

</div>Als erstes lesen wir den Index aus, also welche Zeile der Listbox gerade ausgewählt ist. Dann gehen wir in die Nummernliste und ziehen uns die Nummer heraus, die den ausgewählten Index hat. Also wenn der Nutzer z.B. Zeile 3 auswählt, wird die dritte Nummer herausgesucht. Und abschließend lassen wir uns die Nummer auf dem Nummernlabel anzeigen.

Und damit haben wir es auch schon geschafft.

## ✅ Kompletter Quellcode

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import tkinter as tk

contact_names = list()
contact_numbers = list()


def read_contacts_from_file():
    with open ('contacts.txt','r') as f:
        contact_strings = f.readlines()

    for contact in contact_strings:
        contact = contact.rstrip('\n')
        contact = contact.split(', ')

        contact_names.append(contact[0])
        contact_numbers.append(contact[1])


# Before the window is created, we initially load all contacts from file.
read_contacts_from_file()


def display_number_for_contact():
    i = contact_listbox.curselection()[0]
    number = contact_numbers[i]
    numbers_label['text'] = number


window = tk.Tk()
window.title('Mein Telefonbuch')
window.geometry('300x300')
window.config(bg="lightblue")

numbers_label = tk.Label(text='Hallo!')
numbers_label.config(font=("Arial", 20, "bold"), bg="lightblue")

contact_names_var = tk.StringVar(value=contact_names)
contact_listbox = tk.Listbox(window, height=10, listvariable=contact_names_var)
contact_listbox.bind('<<ListboxSelect>>', lambda e: display_number_for_contact())

numbers_label.pack(pady=10)
contact_listbox.pack()

window.mainloop()

```
```

</div>