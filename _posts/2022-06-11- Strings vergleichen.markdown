# Python Strings vergleichen, Ähnlichkeit messen und ähnlichstes Element finden

Heute möchte ich euch ein paar Funktionen und Konzepte mit an die Hand geben, die man immer wieder gebrauchen kann. Gerade wenn wir Datensätze ergänzen, zusammenfügen oder einfach vergleichen wollen, müssen wir uns damit beschäftigen, wie wir Übereinstimmungen und Ähnlichkeit untersuchen können. Schauen wir uns dazu mal drei passende Problemchen aus der Praxis an und wie man sie löst. Viel Spaß!



## Prüfen, ob zwei Strings gleich sind

Ich hab hier mal zwei Strings erstellt. Die heißen einfach `a` und `b`. Um herzufinden, ob zwei Strings gleich sind, können wir im einfachsten Fall einfach ein doppeltes Ist-Gleich `==` verwenden. 

```python
a = 'Hallo'
b = 'Hallo'

if a == b:
	print('Gleich!')

>>> Gleich!
```

In manchen Fällen will man jetzt aber, dass die Groß-und Kleinschreibung ignoriert wird. Das brauchen wir z.B. dann, wenn wir überprüfen wollen, ob es sich unabhängig von der Groß- und Kleinschreibung trotzdem um das selbe Wort handelt. Und das können wir ganz einfach z.B. mit der Funktion `lower()`machen. Mit dieser werden vor dem Vergleich alle Großbuchstaben zu Kleinbuchstaben umgewandelt und erst danach werden die Wörter verglichen. 

Und so können wir sehen, ob es sich um die gleichen Wörter handelt, egal ob sie Groß- oder Kleingeschrieben sind. 

```python
a = 'Hallo'
b = 'hallo'

if a.lower() == b.lower():
	print('Gleich!')

>>> Gleich!
```

## Achtung: casefold() statt lower()

Das funktioniert an sich wunderbar, perfekt ist die Lösung aber leider noch nicht.

Es gibt nämlich noch eine Methode, die noch zuverlässiger funktioniert und in der Python Dokumentation als bessere Alternative zu lower empfohlen wird. Und die heißt `casefold()`. Diese Methode macht anders als lower wirklich alle Unterschiede zwischen Groß- und Kleinschreibung platt. Und das ist besonders dann nützlich, wenn wir wilde Buchstaben wie das `ß` haben, die ja zum Beispiel gar nicht groß geschrieben werden können. 

In diesem Beispiel soll Python erkennen, dass es sich um das selbe Wort handelt, obwohl ein `ß`vorkommt. Lower würde hier jetzt das `ß`ignorieren und somit nicht erkennen können, dass es sich um das gleiche Wort handelt. 

Casefold hingegen wandelt das `ß` automatisch in ein Doppel-S um, sodass Python hier erkennen kann, dass es sich um das selbe Wort handelt. 

```python
a = 'Außenspiegel'
b = 'AUSSENSPIEGEL'

if a.casefold() == b.casefold():
	print('Gleich!')

>>> Gleich!
```

Wenn wir auf der sicheren Seite sein wollen, sollten wir also Casefold verwenden.

## Ähnlichkeit berechnen

Manchmal wollen wir nicht wissen, ob zwei Texte identisch sind, aber trotzdem wissen, wie sehr sie sich voneinander unterscheiden oder wie ähnlich sie sind. Python hat dafür von Haus aus eine super bequeme Lösung - und zwar den SequenceMatcher. Der ist Teil eines Moduls mit dem Namen `difflib`, dass wir ganz einfach importieren können.

```python
from difflib import SequenceMatcher

satz_a = 'Kommt ein Mensch zum Augenarzt...'
satz_a = 'Kommt ein Zyklop zum Augearzt...'

ratio = SequenceMatcher(a=satz_a, b=satz_b).ratio()
print(ratio)

>>> 0.8
```

Als Ergebnis bekommen wir eine Zahl zwischen 0 und 1 zurück. Und je größer die Zahl ist, desto ähnlicher sind sich die Texte. Und das ist eine Information, die wir in der Praxis immer wieder brauchen, umso geiler also, dass das mal wieder bei Python ziemlich elegant gelöst ist.

## Ähnlichstes Element aus einer Liste finden

Das `difflib`Modul können wir auch nutzen, um aus einer Liste aus Elementen das Element rauszufischen, dass einem bestimmten Element am ähnlichsten ist. 

Ich hab hier ein Ausgangswort, das hab ich einfach `word`genannt. Und ich hab eine Liste aus Wörtern, die meinem Wort mehr oder weniger ähnlich sind. 

Dafür rufe ich jetzt einfach `get_close_matches()`auf. Als erstes in die Klammer kommt mein Ausgangswort. Danach folgt dann die Liste der Wörter, die ich vergleichen möchte.

Mit `n`kann ich hier übrigens festlegen, wieviele Ergebnisse ich zurückbekommen möchte. Und mit `cutoff`kann ich bestimmen, wie ähnlich ein Wort sein muss, um als Ergebnis aufzutauchen. Ich setz hier cutoff mal auf 0.5, sodass nur Wörter auftauchen, die zumindest zu 50% meinem Ausgangswort ähnlich sind.

```python
from difflib import get_close_matches

my_word = 'Affenhaus'

word_list = [
	'Affenhau', 
	'Affenhaus', 
	'Augenschmaus'
	]

results = get_close_matches(my_word, word_list, n=3, cutoff=0.5)
print(results)

>>> ['Affenhaus', 'Affenha', 'Augenschmaus']
```

Als Ergebnis kriege ich jetzt hier die Liste der ähnlichsten Wörter zurück. Das ähnlichste Wort steht dabei ganz am Anfang, in dem Fall hier also "Affenhaus" und das unähnlichste Wort steht entsprechend am Ende.

Das ähnlichste Wort aus der Liste kann ich mir jetzt anzeigen lassen, indem ich einfach auf das erste Element der Liste zugreife.

```python
best_result = results[0]
print(best_result)

>>> Affenhaus
```

Und Python gibt mir hier wie erwartet das Wort `Affenhaus`aus der Liste aus. Und das ist ja auch tatsächlich das Wort, das dem Ausgangswort am ähnlichsten ist. 


