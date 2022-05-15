---
id: 20
title: 'Python MySQL | Daten einfügen | Tutorial (Deutsch) | für Anfängerinnen und Anfänger 🐬'
date: '2021-08-12T10:15:52+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=20'
permalink: /2021/08/12/python-mysql-daten-einfuegen-tutorial-deutsch-fuer-anfaengerinnen-und-anfaenger-%f0%9f%90%ac/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/08/Thumbnail-sql-neu.png'
categories:
    - Datenbanken
---

[Im ersten Tutorial](https://www.youtube.com/watch?v=8s9C4mLFWEc) haben wir uns angeschaut, wie man mit Python eine Datenbank erstellen kann. Und heute wollen wir die Datenbank zum ersten mal mit Daten füllen. Los geht’s!

<iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" frameborder="0" height="315" loading="lazy" src="https://www.youtube.com/embed/RWN08b0tVoM?controls=0" title="YouTube video player" width="560"></iframe>So sieht unser Quellcode bisher aus:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import mysql.connector

my_db = mysql.connector.connect(
    host="localhost",
    user="root",
    password="adsfwioern95203740ß!!?=234yxnücasd..er!"
)

my_cursor = my_db.cursor()

my_cursor.execute("CREATE DATABASE tourplaner")
my_cursor.execute("SHOW DATABASES")

for db in my_cursor:
    print(db)

```
```

</div><div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
('information_schema',)
('mysql',)
('performance_schema',)
('sys',)
('tourplaner',)
```
```

</div>Da wir jetzt dauerhaft in unserer Tourplaner-Datenbank arbeiten werden, können wir die Datenbank mit in unseren Connector eintragen. Alles überflüssige aus dem Skript können wir jetzt auch entfernen.

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
```
```

</div>Jetzt erstellen wir in der Datenbank `tourplaner` eine Tabelle. Das wird dann auch die Tabelle sein, in der wir die tatsächlichen Daten eintragen. Und spätestens jetzt sollten wir uns Gedanken um die Struktur der Daten machen.

Für das Tutorial hab ich mir gedacht, dass wir einen kleinen Tourplaner schreiben, in dem Konzerttermine einer Band gespeichert werden. Dafür hab ich mal ein paar alte Tourdaten meiner Band rausgesucht. Und die sehen folgendermaßen aus:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
11.11.2017 – ISR – Haifa 
10.11.2017 – ISR – Tel Aviv-Jaffa 
09.11.2017 – ISR – Ein Hashofet 
08.11.2017 – ISR – Jerusalem 
06.11.2017 - ISR – Tel Aviv-Jaffa 
```
```

</div>Ihr seht schon – die Tourdaten bestehen immer aus 3 Daten: Dem Konzertdatum, dem Land und der Stadt. Und in dieser Form legen wir jetzt auch unsere Tabelle an. Zuerst erstellen wir einen entsprechenden sql-Befehl.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
sql = """
        CREATE TABLE konzerte(
            datum DATE,
            land TINYTEXT,
            stadt TINYTEXT
            )
      """
```
```

</div>Hinter dem Namen der Spalte geben wir dahinter immer den Datentyp an, z.B. `DATE` für ein Datum. Den sql-Befehl lassen wir jetzt vom Cursor ausführen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
my_cursor.execute(sql)
```
```

</div>Nun hat der Cursor für uns eine neue Tabelle angelegt. Und jetzt können wir auch schon den ersten Datensatz eintragen. Auch dafür schreiben wir wieder einen SQL-Befehl.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
#11.11.2017 – ISR – Haifa 
sql = """
        INSERT INTO konzerte VALUES (
            '2017-12-18',
            'Israel',
            'Tel Aviv'
        )
      """

my_cursor.execute(sql)
my_db.commit()

```
```

</div>Anschließend wollen wir natürlich sehen, ob das funktioniert hat. Deshalb schreiben wir uns eine Funktion, die uns alle Daten der Tabelle ausgibt.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def show_all_data():
    my_cursor.execute("SELECT * FROM konzerte")
    result = my_cursor.fetchall()

    for _ in result:
        print(_)


show_all_data()
```
```

</div>Wenn wir das Skript jetzt ausführen, sehen wir, dass erfolgreich ein neuer Datensatz angelegt wurde. An der Stelle könnten wir jetzt eigentlich schon aufhören. 🥳

 Aber für jeden neuen Datensatz hier direkt im Quellcode herumzufummeln, ist natürlich noch keine schöne Lösung. Deshalb schreiben wir uns jetzt noch eine Funktion, die vom Nutzer den neuen Datensatz einfach abfragt.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def insert_concert_from_user_input():

    datum = input('Datum: ')
    land = input('Land: ')
    stadt = input('Stadt: ')

    val = f'"{datum}", "{land}", "{stadt}"'
    sql = f'INSERT INTO konzerte VALUES ({val})'

    my_cursor.execute(sql)
    my_db.commit()

insert_concert_from_user_input()
```
```

</div>Und damit haben wir es geschafft. Wenn wir das Skript ausführen, können wir bequem einen neuen Datensatz anlegen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
python3 main.py

 Datum: 2017-11-10
 Land: Israel
 Stadt: Tel Aviv
 (datetime.date(2017, 11, 10), 'Israel', 'Tel Aviv')
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

    val = f'"{datum}", "{land}", "{stadt}"'
    sql = f'INSERT INTO konzerte VALUES ({val})'

    my_cursor.execute(sql)
    my_db.commit()


def show_all_data():

    my_cursor.execute("SELECT * FROM konzerte")
    result = my_cursor.fetchall()

    for _ in result:
        print(_)


insert_concert_from_user_input()
show_all_data()

```
```

</div>