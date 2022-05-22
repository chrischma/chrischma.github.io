Ihr habt in den Kommentaren gefragt, ob ich nicht mal ein Video zum Thema list Comprehension machen kann. Und das mach ich natürlich sehr gerne, los geht's!



# Was ist List Comprehension?

Zugegeben: Als ich angefangen habe, Python zu lernen ich mich darum gedrückt, mir List Comprehension mal genauer anzugucken.  Einerseits klingt der Begriff schon mal ziemlich sperrig und die Deutsche Übersetzung, "Listenabstraktion" hat mich auch eher verunsichert als motiviert. Und so richtig geil und intuitiv sehen Codzeilen wie diese hier auch nicht unbedingt aus:

`BEISPIELZEILE`

Dabei ist das Grundprinzip eigentlich ebenso einfach wie genial. Mit List Comprehension können wir mit minimalem Aufwand für eine große Zahl von Elementen in einer Liste etwas bestimmtes machen. Und die Resultate, also die Ergebnisse die dabei entstehen, werden uns direkt in einer neuen Liste gesammelt. 

Der Aufbau ist dabei immer gleich:

```python
[mach_etwas for element in liste]
```

Machen wir das ganze mal etwas konkreter. 

Wir haben eine Liste mit dem Namen "Zahlen" und diese Liste enthält alle Zahlen von 1 bis 10. Und wir wollen List Comprehension jetzt nutzen um alle Zahlen zu verdoppeln.

```python
zahlen = [1,2,3,4,5,6,7,8,9,10]
```

Schauen wir uns erstmal an, wie wir das ganz Oldschool ohne Listcomprehension machen würden. 

```python
verdoppelte_zahlen = [] # Zuerst legen wir eine neue Liste an.

for zahl in zahlen: # Dann gehen wir durch alle Zahlen durch.
    neue_zahl = zahl*2 # Wir verdoppeln jede Zahl und fügen sie dann...
    verdoppelte_zahlen.append(neue_zahl) # der neuen Liste hinzu.
```

Und an der Version ist jetzt auch nichts schlecht oder falsch. Es geht bloß eben doch einfacher - und zwar mit List Comprehension. Probieren wir's mal.

```python
[x*2 for zahl in zahlen]
```

Und tatsächlich, das Ergebnis ist das selbe:

```python
[2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
```

Das ist jetzt natürlich ein recht konstruiertes Beispiel, der eigentlich Spaß liegt aber in Beispielen, wie einem in der Praxis immer mal wieder über den Weg laufen. Schauen wir also mal, wie uns List Comprehension im Alltag Zeit und Nerven sparen kann. Hier kommen ein Paar Beispiele.

# Praxisbeispiel 1 - Währungen umrechnen

Stellt euch ihr hab eine Liste mit 10 Geldbeträgen in USD und wollt die Beträge in Euro umrechnen.

```python
betraege_in_euro = [30.99, 24.95, 9.99, 12.99, 1.50]
```

So eine Umrechnung ist super schnell erledigt.

```python
kurs = 0.94 # USD zu EURO
betraege_in_euro = [30.99, 24.95, 9.99, 12.99, 1.50]

[betrag*kurs for betrag in betraege_in_euro]
```


