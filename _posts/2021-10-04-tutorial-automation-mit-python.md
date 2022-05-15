---
id: 118
title: 'Tutorial: Automation mit Python'
date: '2021-10-04T15:08:33+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=118'
permalink: /2021/10/04/tutorial-automation-mit-python/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/10/Thumbnail-automatisierung.png'
categories:
    - 'Bots und Automatisierung'
---

<figure class="wp-block-embed is-type-video is-provider-youtube wp-block-embed-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" frameborder="0" height="387" loading="lazy" src="https://www.youtube.com/embed/gRMbCvQgOoU?feature=oembed" title="Python Tutorial: 🌍 Web-Automatisierung mit Selenium  | Einfaches Tutorial für Neulinge (Deutsch)" width="688"></iframe></div></figure>Immer wieder werde ich in den Kommentaren gefragt, wie man einen Browser fernsteuern kann. Und genau das lernen wir heute. Ich bin Chris – und das ist Programmieren mit Chris. Viel Spaß!

Das Zauberwort für solche Aufgaben lautet Automation. Dank Automation können wir fast jede Art von Nutzerinterkation auf einer Website simulieren. Wir können also Websiten aufrufen, uns auf Seiten einloggen, bestimmte Tasten drücken, Scrollen, Texte posten, Bilder liken, Aktien verkaufen, Arzttermine buchen usw. Und das beste: Die Befehle, die wir dafür brauchen, sind immer die gleichen, egal ob wir auf Ebay, Amazon oder jeder anderen Seite sind. Wir machen das heute am Beispiel der Wikipedia, weil man anhand dieser Seite die Grundlagen besonders leicht lernen kann.

Alles was wir dafür brauchen ist ein halbwegs aktueller Webbrowser, also z.B. Google Chrome und ein sogeannter Webdriver. Ein Webdriver macht es möglich, dass die Befehle, die wir z.B. mit Python programmieren, vom Browser ausgeführt werden können.

Wichtig dabei: Der Webdriver und der Browser müssen die selbe Version haben. Schauen wir deshalb mal nach, welche Version von Chrome wir eigentlich haben.

Mit der Versionsnummer im Gepäck gehen laden wir uns jetzt einen Webdriver herunter. Dafür gehen wir auf `chromedriver.chromium.org`, den Link findet ihr wie immer in der Videobeschreibung.

Hier finden wir jetzt die passende Version und laden sie herunter.

Als nächstes wählen wir unser Betriebssystem aus. Bei mir ist das jetzt MacOS mit M1 Prozessor, wenn ihr aber z.B. Windows wählt ihr hier einfach die Windows-Version.

Weiter geht es jetzt im Quellcode.

Als nächstes installieren wir die benötigten Module. Wir verwenden heute die Module `time`und `selenium`. time ist immer schon vorinstalliert, selenium noch nicht. Deshalb gehe ich in mein Terminal und tippe ein:

`pip3 install selenium`

Und dann können wir uns beide Module auch gleich importieren. Ich gehe also in mein Skript und tippe ein:

```
<pre class="wp-block-preformatted">import time<br></br>from selenium import webdriver
```

Als nächstes müssen wir unserem Computer mitteilen, wo sich die Webdriver datei befindet. Und ich finde es immer ganz praktisch, wenn der Webdriver einfach mit im Projektordner liegt. Ich ziehe jetzt also einfach die Webdriver-Datei in den Hauptordner des Projektes. Und jetzt gebe ich Bescheid, dass sich genau dort die Webdriver-Datei befindet.

`driver = webdriver.Chrome('./chromedriver')`

Und jetzt können wir auch schon eine Website aufrufen. Websiten öffnen wir immer mit dem Befehl `get`.

`driver.get('https://www.wikipedia.de')`

Als nächstes macht es Sinn, eine kleine Verzögerung einzubauen. Einerseits gehen wir damit sicher, dass die Seite auch wirklich vollständig geladen wird, bevor wir mit ihr interagieren. Und außerdem lässt das unsere Interaktionen für die Website menschlicher wirken. Und das ist natürlich praktisch, um nicht als Bot erkannt zu werden.

`time.sleep(5)`

Jetzt wollen wir in die Suchleiste einen Begriff eingeben. Tastatureingaben können wir auch ganz einfach über unseren Webdriver schicken, wir müssen vorher allerdings festlegen, wo der Text eingegeben werden soll.

Dafür mache ich auf das Element, mit dem ich interagieren will, einen Rechtsklick und klicke auf ‚Untersuchen‘.

Jetzt wird mir das Element im Quellcode angezeigt. Und hier sieht man schon, dass die Suchleisten sowohl einen namen als auch eine id hat. Und über beides könnte ich die Suchleiste jetzt identifizieren. Wir machen das mal am Beispiel der id.

`search_bar = driver.find_element_by_id('txtSearch')`

Als nächstes lassen wir automatisiert etwas in die Suchleiste eintippen. Und das funktioniert mit dem Befehl `send_keys`.

`search_bar.send_keys('Salzburg')`

Wir könnten jetzt übrigens einfach noch eine Enter-Taste hinterherschicken, um unsere Eingabe zu bestätitigen. Ich möchte euch aber stattdessen zeigen, wie man auf Suchen-Button klickt, damit ihr auch das mit dem Klicken schon einmal gesehen habt. Auch dafür suche ich wieder das Element und untersuche es. Wie ihr seht, hat das Element jetzt weder einen namen noch eine id. Ist aber kein Problem, denn wir können die Suchleiste immer noch über ihre Klasse identifizieren. Die Klasse heißt einfach search-icon und diese Information nehmen wir uns mit in unser Skript.

`search_button = driver.find_element_by_class_name('search-icon')`

Und jetzt müssen wir nur noch Klicken. Das geht passenderweise mit der Click-Funktion.

`search_button.click()`

Unser bot kann jetzt also schon klicken und Seiten aufrufen. Und jetzt lesen wir spaßenshalber noch Informationen aus der Website aus.

Sagen wir also, wir wollen den gesamten Artikel kopieren. Auch dafür untersuche ich wieder die Website. Offensichtlich hat der Artikel die Klassenbezeichnung `mw-body`. Und über diese kann ich das Element jetzt wieder finden.

`page = driver.find_element_by_class_name('mw-body')`

Den Text lasse ich mir dann anschließend ausgeben und beende dann den Webdriver.

`print(page.text)`

`driver.quit()`

\[ausprobieren\]

Okay, soviel erstmal für heute. Fragen und Wünsche könnt ihr wie immer in der Kommentarspalte dalassen, ich antworte bei passenden Fragen mit kurzen Videoantworten. Und jetzt viel Spaß beim Ausprobieren, bleibt neugierig und bis bald!

## ✅ Kompletter Quellcode

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import time
from selenium import webdriver
​
driver = webdriver.Chrome('./chromedriver')
​
driver.get('https://www.wikipedia.de')
time.sleep(5)
​
search_bar = driver.find_element_by_id('txtSearch')
search_bar.send_keys('Salzburg')
search_button = driver.find_element_by_class_name('search-icon')
search_button.click()
​
page = driver.find_element_by_class_name('mw-body')
print(page.text)
​
driver.quit()
```
```

</div>