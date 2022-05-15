---
id: 108
title: 'Python MySQL Daten ändern'
date: '2021-10-04T13:49:48+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=108'
permalink: /2021/10/04/python-mysql-daten-aendern/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/08/Thumbnail-sql-neu.png'
categories:
    - Datenbanken
---

Hinweis: [Hier](https://christoph-schmalfuss.de/blog/2021/08/12/python-mysql-daten-einfuegen-tutorial-deutsch-fuer-anfaengerinnen-und-anfaenger-%f0%9f%90%ac/) findest du einen weiteren Artikel zum Thema MySQL, den du idealerweise vorher gelesen hast.

<figure class="wp-block-image size-large">[![](http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/08/Thumbnail-sql-neu-1024x576.png)](https://youtu.be/2YhGjO_F1Ls)</figure>In diesem Artikel schauen wir uns an, wie man mit Python Daten in einer MySQL-Datenbank ändern kann. Viel Spaß!

Der SQL-Befehl, um einen Datensatz zu ändern, besteht grundsätzlich aus drei Teilen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-sql" data-lang="SQL">```
UPDATE konzerte
SET stadt = 'Akkon'
WHERE stadt = 'Haifa'
```
```

</div>Am Anfang steht der Befehl UPDATE und der Name der Tabelle, in der wir arbeiten. In unserem Beispiel heißt die Tabelle konzerte.

Als nächstes folgt der SET-Befehl. Mit diesem setzen wir einen neuen Wert in die Tabelle ein und überschreiben damit den alten Wert.

Und mit dem WHERE-Befehl legen wir fest, welche Bedingung erfüllt sein muss. Hier habe ich festgelegt, dass der Datensatz überschrieben wird, bei dem die Stadt Haifa eingetragen ist.

Wir können das ja mal mit Python ausprobieren. Den alten Befehl vom letzten Mal löschen wir erstmal raus.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
# insert_concert_from_user_input()
```
```

</div>Jetzt können wir den SQL-Befehl festlegen. Den müssen wir dann nur noch ausführen und bestätigen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
sql = 'UPDATE konzerte SET stadt = "München" WHERE stadt = "Akkon"' # Befehl festlegen
my_cursor.execute(sql) # ausführen
my_db.commit() # bestätigen
```
```

</div>Es ist aber natürlich bisschen blöd, wenn wir für jede Änderung in der Datenbank unseren Quellcode anpassen. Deshalb macht es Sinn, eine Funktion zu schreiben, die dem Nutzer diese Arbeit erspart. Ich zeig euch mal an einem Beispiel, wie so eine Funktion aussehen könnte.

Wir schreiben einen kleinen Dialog für den Nutzer, der nach der alten Stadt fragt, die ersetzt werden soll und nach der neuen Stadt fragt, die eingefügt werden soll:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def update_city():
    old_city = input('Welche Stadt soll ersetzt werden? ')
    new_city = input('Welche Stadt soll stattdessen eingetragen werden? ')

```
```

</div>Aus diesen Eingaben bauen wir jetzt einen SQL-Befehl. Auch den führen wir wieder aus und bestätigen ihn.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
    sql = f'UPDATE konzerte SET stadt = "{new_city}" WHERE stadt = "{old_city}"'
    my_cursor.execute(sql)
    my_db.commit()
```
```

</div>Anschließend rufen wir die Funktion auf.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
update_city():
```
```

</div>Wenn wir das Skript jetzt ausführen, sollte das eigentlich alles schon gut funktionieren. Probieren wir es aus!

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
Welche Stadt soll ersetzt werden? Haifa
Welche Stadt soll stattdessen eingetragen werden? Döbeln
(datetime.date(2017, 11, 11), 'Israel', 'Döbeln')
(datetime.date(2017, 11, 10), 'Israel', 'Tel Aviv')

Process finished with exit code 0
```
```

</div>## ✅ Kompletter Quellcode

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import mysql.connector

my_db = mysql.connector.connect(
    host="localhost",
    user="root",
    password="adsfwioern95203740ß!!?=234yxnücasd..er!",
    database="tourplaner"
)

my_cursor = my_db.cursor()


def insert_concert_from_user_input():

    datum = input('Datum: ')
    land = input('Land: ')
    stadt = input('Stadt: ')

    val = f'"{datum}", "{land}", "{stadt}'
    sql = f'INSERT INTO konzerte VALUE ({val})'

    my_cursor.execute(sql)
    my_db.commit()


def show_all_data():
    my_cursor.execute("SELECT * FROM konzerte")
    result = my_cursor.fetchall()

    for _ in result:
        print(_)


def update_city():
    old_city = input('Welche Stadt soll ersetzt werden? ')
    new_city = input('Welche Stadt soll stattdessen eingetragen werden? ')

    sql = f'UPDATE konzerte SET stadt = "{new_city}" WHERE stadt = "{old_city}"'
    my_cursor.execute(sql)
    my_db.commit()


update_city()
show_all_data()
```
```

</div>