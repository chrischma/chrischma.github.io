---
id: 365
title: 'Eingeloggt bleiben &#8211; Python Selenium | Login dauerhaft speichern'
date: '2022-04-24T13:35:15+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=365'
permalink: /2022/04/24/python-login-speichern-eingeloggt-bleiben-mit-selenium/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Thumbnail-selenium-login.png'
categories:
    - 'Bots und Automatisierung'
    - Selenium
---

Das ständige Einloggen auf Websites kann beim Automatisieren und beim Webscraping viel Zeit und nerven kosten. Deshalb schauen wir uns heute mal an, wie man so einen Login speichern und überspringen kann. Und um eine Frage gleich mal vorweg zu beantworten: Ja, das Prinzip funktioniert auf fast allen Websites. Viel Freude mit dem Video, los geht’s!

<figure class="wp-block-image size-large">![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Thumbnail-selenium-login-1024x1024.png)</figure>## Vorbereitung – Module importieren

So ein Login funktioniert eigentlich immer gleich. Wir gehen auf eine Website, geben unsere Daten ein und dann wird unser Login einem entsprechenden Cookie gespeichert. Und wenn wir den Cookie erstmal gespeichert haben, bleibt der in der Regel mehrere Jahre gültig, sodass wir uns zukünftig nicht mehr einloggen müssen, sondern einfach den Cookie laden, den wir einmalig gespeichert haben. Und genau das ist auch das, was wir jetzt als erstes machen.

Um das ganze mit Python umzusetzen, verwenden wir natürlich Selenium, damit wir unseren Browser fernsteuern können. Und da unsere Cookies im JSON-Format gespeichert werden, brauchen wir außerdem das Modul json. Wie genau das JSON-Format funktioniert, müsst ihr an dieser Stelle gar nicht wissen – ich verlink euch für den Fall der Fälle trotzdem unten in der Videobeschreibung ein Video, das das Ganze bisschen genauer erklärt.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from selenium import webdriver
import json
```
```

</div>## Plattform festlegen

Zunächst müssen wir natürlich die Cookies speichern, um sie später laden zu können. Dafür leg ich direkt mal fest, in welcher **Datei** meine Cookies eigentlich gespeichert werden sollen.

Außerdem lege ich eine **Start URL** fest. Das ist die Internetseite, auf der ich später Anfangen will, mit Selenium zu surfen. Üblicherweise ist das einfach die Startseite der jeweiligen Plattform. Ich zeig euch das heute am Beispiel Twitter, deshalb lege ich als Start-URL die Startseite von Twitter fest. Wenn ihr das gleich für eine andere Website machen wollt, schreibt ihr also diese Website hier einfach rein.

Und zu guter letzt legen wir auch gleich unseren Webdriver an, um dann den Browser fernzusteuern.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
cookies_file = 'twitter-cookies.json'
start_url = 'https://www.twitter.com'
driver = webdriver.Chrome()
```
```

</div>## Cookies speichern

Für das Speichern der Cookies brauchen wir natürlich erstmal eine Funktion, die das für uns erledigt. Und der Funktion übergeben wir dann unseren Webdriver, den wir gerade benutzen. Der wird dann wie immer einfach driver heißen, deshalb schreibe ich in die Klammern „driver“.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def save_cookies(driver):
```
```

</div>Der Webdriver soll dann als erstes mal auf unsere Startseite gehen, damit wir uns bequem einloggen können. Und das machen wir mit der Funktion driver.get()

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def save_cookies(driver):
    driver.get(start_url)
```
```

</div>Anschließend soll der Driver warten, bis wir uns eingeloggt haben und erst dann die Cookies abspeichern. Und das lösen wir hier so, dass der User einfach Enter drücken soll, sobald er fertig mit einloggen ist – und erst dann werden die Cookies gespeichert.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
	input('Press RETURN to save cookies!')
```
```

</div>Und jetzt wird unser Skript also so lange nichts machen, bis wir Enter gedrückt haben.

Als nächstes legen wir fest, was passieren soll, nachdem wir Enter gedrückt haben. Dann sollen ja die Cookies vom Webdriver ausgelesen werden und dafür gibt es die Funktion get\_cookies()

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
	cookies = driver.get_cookies()
```
```

</div>Jetzt sind die Cookies ausgelesen. Blöderweise werden uns die Daten allerdings als Python Objekt und nicht als JSON zurückgegeben, deshalb machen wir aus dem Python Objekt jetzt einen schönen JSON string.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
	cookies = json.dumps(cookies)
```
```

</div>Um später auf die Cookies zugreifen zu können, speichern wir die Cookies in einer Datei.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
	with open(cookies_file, 'w') as f:
		f.write(cookies)
```
```

</div>Und wenn wir fertig sind mit dem ganzen Bumms, dann schließen wir einfach unseren Browser.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
driver.quit()
```
```

</div>Unsere Funktion ist fertig und kann jetzt auch schon ausgeführt werden. Dafür rufe ich die Funktion einfach auf.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
save_cookies(driver)
```
```

</div><div class="hcb_wrap">```
<pre class="prism line-numbers lang-json" data-lang="JSON">```
Nachdem wir das Skript aufgerufen haben, speichert Python alle wichtigen Daten in unserer .json-Datei. 

[{"domain": ".twitter.com", "expiry": 165088791156, "httpOnly": true, ...
```
```

</div>## Cookies laden

Der Login ist jetzt in unserer JSON-Datei gespeichert. Und anstatt uns zukünftig immer einzuloggen, schreiben wir jetzt eine Funktion, die automatisch den vorhanden Login-Cookie aus unserer Datei lädt und so den Login überspringt.

Dazu öffnen wir zu allererst die Datei und holen uns die Daten heraus.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def load_cookies(driver):
	with open(cookies_file, 'r') as f:
		cookies = json.load(f)
```
```

</div>Anschließend wollen wir, dass unser Webdriver bequem direkt zur Startseite navigiert.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
	driver.get(start_url)
```
```

</div>Und wenn der Browser dann auf der Startseite angekommen ist, sollen alle Cookies zum aktuellen Webdriver hinzugefügt werden. Dafür bietet sich eine kleine for-Schleife an. Und die sorgt dafür, dass Python durch alle gespeicherten Cookies geht und sie dem Webdriver hinzufügt.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
	for cookie in cookies:
		driver.add_cookie(cookie)
```
```

</div>Und wenn dann alle Cookies geladen sind, soll die Seite nochmal aktualisiert werden, damit wir nicht mehr die alte Seite sehen, sondern die Version der Seite, bei der wir schon eingeloggt sind.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
	driver.refresh()
```
```

</div>Und als letztes geben wir jetzt einfach den driver mitsamt Cookies wieder zurück, sodass wir mit dem driver dann eingeloggt alle anderen Dinge tun können, die wir so vorhaben.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
   return driver
```
```

</div>## Skript ausführen

Jetzt, da unsere Cookies schon gespeichert sind, brauchen wir die save Funktion nicht mehr. Ich lasse sie trotzdem noch gespeichert, falls wir sie später noch einmal brauchen, lösche aber die Zeile raus, in der die Funktion wirklich aufgerufen wird (`save_cookies(driver)`).

Stattdessen rufe ich jetzt die load\_cookies Funktion auf. Und das Ergebnis der Funktion, also meinen eingeloggten Webdriver, speichere ich mir direkt in der Variable `driver`, mit der ich dann beliebig eingeloggt weiterarbeiten kann. Und wenn ich das Skript jetzt ausführe, loggt sich der Browser für mich automatisch ein und mir bleibt für die nächsten Jahre erstmal das Einloggen erspart.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
driver = load_cookies(driver)
```
```

</div>Und so einfach ist es also, sich mit Selenium dauerhaft einzuloggen.

## ✅ Kompletter Quellcode

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from selenium import webdriver
import json


cookies_file = 'twitter-cookies.json'
start_url = 'https://www.twitter.com'
driver = webdriver.Chrome()


def save_cookies(driver):
	driver.get(start_url)
	input('Press RETURN to save cookies!')

	cookies = driver.get_cookies()
	cookies = json.dumps(cookies)

	with open(cookies_file, 'w') as f:
		f.write(cookies)

	driver.quit()


def load_cookies(driver):
	with open(cookies_file, 'r') as f:
		cookies = json.load(f)

	driver.get(start_url)
	
	for cookie in cookies:
		driver.add_cookie(cookie)

	driver.refresh()

	return driver


# save_cookies(driver) 
driver = load_cookies(driver)
```
```

</div>