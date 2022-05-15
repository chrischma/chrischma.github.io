---
id: 94
title: 'Python: Argumente parsen (CLI)'
date: '2021-09-28T09:50:01+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=94'
permalink: /2021/09/28/python-argumente-parsen-cli/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/10/Thumbnail-argparse.png'
categories:
    - 'MacOS und Linux'
---

<figure class="wp-block-image size-large">![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2021/10/Thumbnail-argparse-1024x576.png)</figure>Bestimmt habt ihr schon mal Python Programme benutzt, denen man gleich beim starten noch bestimmte Werte mitgeben kann. Und genau so ein Skript wollen wir heute schreiben. Ich bin Chris und das ist Programmieren mit Chris. Viel Spaß.

Das Video hier ist in Zusammenarbeit mit dem lieben Felix von [Hello Coding ](https://hellocoding.de/blog/coding-language/python/cli-command-in-python)entstanden. Mehr dazu erzähle ich am Ende des Videos, wir steigen erstmal in den Inhalt ein.

Normalerweise starten wir Python Programme ja z.B. mit Befehlen wie diesem hier:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
python3 hello.py
```
```

</div>Unser Ziel ist es, dass wir ein Programm schreiben, dem wir Argumente mitgeben können.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
python3 hello.py --name Chris
```
```

</div>Damit Python das Argument lesen kann, müssen müssen wir die angegebenen Argumente analysieren. Oder anders ausgedrückt: Wir müssen sie parsen. Passenderweise nutzen wir dafür das Modul `argparse`.

Okay, legen wir im Quellcode los.

Ich hab jetzt schon mal eine leere Python Datei erstellt. Die trägt den Namen `hello.py`.

Wie immer importiere ich zuerst die benötigten Module.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import argparse
```
```

</div>Als nächstes lege ich die Grundstruktur meines Skriptes an. Als erstes brauchen wir eine main Funktion. In dieser erstellen wir gleich einen Parser und legen unsere Argumente an.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def main():
    parser = argparse.ArgumentParser()
    parser.add_argument('--name')
    
    args = parser.parse_args()
    print(args)
```
```

</div>Die Main-Funktion soll jetzt immer aufgerufen werden, wenn das Programm gestartet wird. Das legen wir am Ende des Dokumentes fest.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
if __name__ == "__main__":
    main()
```
```

</div>Das Auslesen der Argumente funktioniert schon mal. Jetzt basteln wir eine neue Funktion, die die Argumente weiter verarbeitet. Wir sorgen jetzt dafür, dass der Name, den der Nutzer eintippt, in der ausgegebenen Begrüßung auftaucht. Ich füge deshalb meiner Main-Funktion erstmal eine neue Funktion mit dem Namen `say_hello` hinzu.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def main():
    parser = argparse.ArgumentParser()
    parser.add_argument('--name')
    
    args = parser.parse_args()
    say_hello(args)
```
```

</div>Über der Main-Funktion lege ich jetzt die say\_hello-Funktion an.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def say_hello(args):
    if args.name:
        print(f'Hallo {args.name}!')

    else:
        print('Hallo unbekannter Freund!')

```
```

</div>So sollte das Ganze jetzt schon funktionieren. Probieren wir’s aus!

Und jetzt hatte ich ja noch versprochen, einige Worte zu Felix zu sagen. Felix betreibt den Programmier-Blog Hello Coding, wo er inzwischen schon eine Menge Tutorials veröffentlicht hat. Felix hat sich auch mit dem Thema dieses Videos beschäftigt, sein Artikel geht aber fachlich noch ein bisschen weiter. Wenn ihr also noch tiefer in das Thema einsteigen wollt, dann findet ihr den passenden Artikel [hier](https://hellocoding.de/blog/coding-language/python/cli-command-in-python). Lasst uns gern auch hier auf YouTube oder in Felix Blog einen Kommentar da, ob das für euch hilfreich ist und ob ihr euch zukünftig noch mehr solcher gemeinsamen Inhalte wünscht.

Okay, soviel aber erstmal für heute. Wenn ihr den Kanal unterstützen wollt, dann findet ihr alle Infos dazu in der Videobeschreibung. Jetzt wünsch ich euch ganz viel Spaß beim Ausprobieren, bleibt neugierig und bis bald!

## ✅ Kompletter Quellcode

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import argparse


def say_hello(args):
    if args.name:
        print(f'Hallo {args.name}!')

    else:
        print('Hallo unbekannter Freund!')


def main():
    parser = argparse.ArgumentParser()
    parser.add_argument('--name')
    
    args = parser.parse_args()
    say_hello(args)


if __name__ == "__main__":
    main()
```
```

</div>