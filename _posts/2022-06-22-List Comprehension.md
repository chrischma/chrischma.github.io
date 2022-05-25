Ihr habt in den Kommentaren gefragt, ob ich mich mal um das Thema List Comprehension kümmern könnte. Und das mach ich natürlich sehr gerne, los geht's!

# Was ist List Comprehension?

Zugegeben: Als ich angefangen habe, Python zu lernen, hab ich mich lange darum gedrückt, mir List Comprehension mal genauer anzugucken.  Einerseits klingt der Begriff schon mal ziemlich sperrig und die Deutsche Übersetzung, "Listenabstraktion" hat mich auch eher verunsichert als motiviert. Und so richtig geil und intuitiv sehen Codzeilen wie diese hier auch nicht unbedingt aus:

```python
[print(film) for film in filme if '2015' in film]
```

Dabei ist das Grundprinzip eigentlich ebenso einfach wie genial. Mit List Comprehension können wir mit minimalem Aufwand für eine große Zahl von Elementen in einer Liste etwas bestimmtes machen. Und die Resultate, also die Ergebnisse die dabei entstehen, werden uns direkt in einer neuen Liste gesammelt, mit der wir dann weiterarbeiten können.

Der Aufbau ist dabei immer gleich:

```python
[mach_etwas for element in liste]
```

Machen wir das ganze mal etwas konkreter. 

Wir haben eine Liste mit dem Namen "Zahlen" und diese Liste enthält alle Zahlen von 1 bis 10. Und wir wollen List Comprehension jetzt nutzen um alle Zahlen zu verdoppeln.

```python
zahlen = [1,2,3,4,5,6,7,8,9,10]
```

Schauen wir uns erstmal an, wie wir das ganz Oldschool ohne List-Comprehension machen würden. 

```python
verdoppelte_zahlen = [] # Zuerst legen wir eine neue Liste an.

for zahl in zahlen: # Dann gehen wir durch alle Zahlen durch.
    neue_zahl = zahl*2 # Wir verdoppeln jede Zahl und fügen sie dann...
    verdoppelte_zahlen.append(neue_zahl) # der neuen Liste hinzu.
```

Und an der Version ist jetzt auch nichts schlecht oder falsch. 

Es geht bloß eben noch einfacher - und zwar mit List Comprehension. Probieren wir's mal.

```python
[x*2 for zahl in zahlen]
```

Und tatsächlich, das Ergebnis ist das selbe:

```python
[2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
```

Das ist jetzt natürlich ein recht konstruiertes Beispiel, der eigentlich Spaß liegt aber in Beispielen, die einem in der Praxis immer mal wieder über den Weg laufen. Schauen wir also mal, wie uns List Comprehension im Alltag Zeit und Nerven sparen kann. Hier kommen ein Paar Beispiele.

# Praxisbeispiel 1 - Währungen umrechnen

Stellt euch vor, ihr hab eine Liste mit 10 Geldbeträgen in USD und wollt die Beträge in Euro umrechnen.

```python
betraege_in_euro = [100, 150, 240, 76, 140]
```

So eine Umrechnung ist super schnell erledigt. Dafür legen wir einfach den Wechselkurs fest und multiplizieren alle Elemente der Liste mit dem Wechselkurs.

```python
kurs = 0.94 # USD zu EURO
betraege_in_euro = [100, 150, 240, 76, 140]

[betrag*kurs for betrag in betraege_in_euro]

# Ergebnis: [94.0, 141.0, 225.6, 71.44, 131.6]
```

# Praxisbeispiel 2 - Listen filtern

In diesem Beispiel haben wir recht lange Liste von Serien.

```python
serien = [
    'Fargo (2014)', 
    'Dekalog (1989)', 
    'Cowboy Bebop (1998)', 
    'Friends (1994)', 
    'When They See Us (2019)', 
    'Willkommen in Gravity Falls (2012)', 
    'Last Week Tonight with John Oliver (2014)', 
    'Nathan for You (2013)', 
    'Unbekanntes Afrika (2013)', 
    'Monty Pythons Flying Circus (1969)', 
    'Der Krieg (2009)', 
    'TVF Pitchers (2015)', 
    'Its Always Sunny in Philadelphia (2005)', 
    'Das Boot (1985)', 
    'Better Call Saul (2015)', 
    'Taskmaster (2015)', 
    'Lass es, Larry! (2000)'
    ]


```

Und unser Job ist es hier, alle Serien aufzulisten, die 2015 erschienen sind. Dafür können wir in unsere List Comprehension einfach einen Filter einbauen. Die Jahreszahl steht immer hinter der Serie in Klammern und dementsprechend können wir hier also einfach nach der Jahreszahl suchen. 

```python
[print(serie) for serie in serien if '2015' in serie]
```

```python
TVF Pitchers (2015)
Better Call Saul (2015)
Taskmaster (2015)
```

# Praxisbeispiel 3 - Strings säubern

Ebenso einfach können wir Teile von Texten entfernen und verändern. Dafür schnappen wir uns nachmal die Serienliste und versuchen jetzt mal, alle Jahreszahlen zu entfernen. Dazu teilen wir jeden Serientitel an der Stelle, wo die Jahreszahl beginnt und behalten dann nur den ersten Teil des Titels. Und da jede Jahreszahl mit einer sich öffnenden Klammer beginnt, können wir genau dort jeden Listeneintrag teilen.

```python
[serie.split('(')[0] for serie in serien]
```

Als Ergebnis bekommen wir eine hübsche und gesäuberte Liste zurück:

```python
['Fargo ', 'Dekalog ', 'Cowboy Bebop ', 'Friends ', 'When They See Us ', 'Willkommen in Gravity Falls ', 'Last Week Tonight with John Oliver ', 'Nathan for You ', 'Unbekanntes Afrika ', 'Monty Pythons Flying Circus ', 'Der Krieg ', 'TVF Pitchers ', 'Its Always Sunny in Philadelphia ', 'Das Boot ', 'Better Call Saul ', 'Taskmaster ', 'Lass es, Larry! ']
```

# Zusammenfassung

Wie ihr sehen könnt, ist so eine List Comprehension also gar nicht so kompliziert, wie es vielleicht auf den ersten Blick scheint. Ich finde, man muss sich vielleicht am Anfang ein wenig an den grundsätzlichen Aufbau gewöhnen. Wenn der aber einmal drin ist, kann man mit List Comprehension wirklich sehr viel Spaß haben. 

Ich empfehle euch deshalb: Schaut euch mal die ein oder anderen Codezeilen an, die ihr bisher  in euren eigenen Projekten geschrieben habt und probiert einfach etwas herum, wie diese Codezeilen mit einer List Comprehension umgesetzt werden könnten. So kriegt ihr ziemlich schnell ein Gefühl dafür, wo List Comprehension Sinn macht und wo nicht. 

Ich wünsch euch jetzt auf jeden Fall ganz viel Spaß beim Ausprobieren, bleibt neugierig und bis bald.
