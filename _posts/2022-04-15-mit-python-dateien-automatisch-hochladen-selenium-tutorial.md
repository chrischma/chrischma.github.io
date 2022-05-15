---
id: 338
title: 'Python Selenium &#8211; Dateien automatisch hochladen'
date: '2022-04-15T13:18:26+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=338'
permalink: /2022/04/15/mit-python-dateien-automatisch-hochladen-selenium-tutorial/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Thumbnail-Dateien-hochladen.png'
categories:
    - 'Bots und Automatisierung'
    - Linux
    - MacOS
    - Selenium
---

<figure class="wp-block-image size-large">![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Thumbnail-Dateien-hochladen-1024x576.png)</figure>Hallo und herzlich willkommen zurück!

Heute wollen wir uns mal anschauen, wie man mit Python Dateien automatisiert auf Webseiten hochladen kann. Ich zeig euch das anhand der Website file-upload.net, das Prinzip das ihr gleich kennenlernt funktioniert aber genau so auch auf 99% der anderen Websites, die man so online finden kann. Den Quellcode, einen passenden Artikel und die Timecodes gibt’s wie immer in der Beschreibung, springt also gern zu den Teilen des Videos, die für euch interssant sind. Viel Freude!

## Wie funktioniert ein Dateiupload?

Wie immer schauen wir uns als erstes an, wie eigentlich der Prozess genau aussieht, den wir automatisieren wollen. Und um eine Datei auf einer Webseite hochzuladen, machen wir ja natürlich erstmal unseren Browser auf, gehen auf unsere Ziel-Webseite klicken dann auf einen Uploadbutton, wählen die Datei aus und bestätigen das.

Das sind also erstmal die Schritte, die wir als Mensch durchführen würden. Und da können wir uns jetzt eigentlich direkt daran machen, die Schritte im Quellcode umzusetzen.

## Module importieren und Variablen festlegen

Als erstes importiere ich jetzt die Module, die wir heute brauchen. Einerseits ist natürlich der Selenium Webdriver, der für uns den Browser fernsteuert und andererseits brauchen wir noch die Klasse „By“, mit der wir Elemente auf der Website identifizieren können.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from selenium import webdriver
from selenium.webdriver.common.by import By
```
```

</div>Als nächstes legen wir fest, auf welcher Website wir unsere Datei hochladen und natürlich um welche Datei es eigentlich geht.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
url = 'https://www.file-upload.net/'
file = '/Users/Chris/thumnail windows.jpg'
```
```

</div>## Website aufrufen

Nachdem geklärt ist, welche Website wir öffnen wollen, können wir unseren Webdriver jetzt auch schon losschicken. Dafür lege ich jetzt meinen Webdriver an…

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
driver = webdriver.Chrome()
driver.get(url)
```
```

</div>… und schicke ihn direkt auf die Website.

## Uploadfeld finden

So ein Dateiupload geschieht in der Regel über ein Input Element. Das unterscheidet sich auch eigentlich nicht von anderen Eingabefeldern, außer dass es den Typ „File“ besitzt. Und genau danach können wir jetzt im Quellcode suchen.

<figure class="wp-block-image size-large">![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Bildschirmfoto-2022-04-15-um-14.54.02-1024x615.png)</figure>Dafür klicke ich einfach auf den Upload Bereich und suche dann nach einem Input Element, dass den Typ „File“ besitzt.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-html" data-lang="HTML">```
<input class="bf-upload-file-input" type="file" name="file" multiple="multiple">
```
```

</div>An dieser Stelle vielleicht kleiner Hinweis: Auf manchen Websites, also z.B. beim Videoupload auf TikTok, ist das Input-Element versteckt, sodass wir damit nicht interagieren können. Sollte das der Fall sein, müssen wir das Element erst sichtbar machen, bevor wir damit Dateien hochladen können. Das ist aber unkompliziert, das entsprechende Video verlinke ich euch unten in der Videobeschreibung.

## Uploadfeld Datei an das Uploadfeld schicken

Mein Uploadfeld kenn ich jetzt, es wird also allerhöchste Zeit, dass wir unsere Datei an das Feld schicken. Und da gibt es eigentlich nur eine Sache, die man verstehen muss. Ich hab ja gerade schon erwähnt, dass so ein Datei-Uploader eigentlich nichts anderes ist als ein Eingabefeld. Und um etwas in ein Eingabefeld zu schreiben, kennen wir ja schon den Befehl send\_keys.

Und genau weil ein Dateiupload eigentlich einfach ein Eingabefeld, ist können wir uns auch den ganzen Upload-Dialog sparen, sondern können den Link zur Datei auf unserem Computer einfach mit dem üblichen Befehl „send\_keys“ an das Feld schicken. Von unserem Dateiupload kennen wir ja zumindest den Namen der Klasse, und daran können wir das Feld jetzt auch eindeutig identifizieren.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
upload_field = driver.find_element(By.CLASS_NAME, 'bf-upload-file-input')
upload_field.send_keys(file)
```
```

</div>Je nach Website müssen wir den Upload übrigens noch bestätigen und das würde mit folgendem Code funktionieren:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
upload_field.submit()
```
```

</div>Und wenn wir das jetzt ausführen, sollte unsere Datei auch schon hochgeladen werden. Für unsere Website brauchen wir den Befehl nicht, aber ich wollte ihn euch zumindest zeigen, damit ihr die Lösung parat habt, falls sich bei eurem Dateiupload nichts tut.

Und damit haben wir’s auch schon geschafft – so einfach ist es also, Dateien mit Selenium auf Webseiten hochzuladen. Ich wünsch euch jetzt noch eine wunderbare Woche, bleibt neugierig und bis bald!

## ✅ Kompletter Quellcode

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from selenium import webdriver
from selenium.webdriver.common.by import By


url = 'https://www.file-upload.net/'
file = '/Users/Chris/thumnail windows.jpg'

driver = webdriver.Chrome()
driver.get(url)

upload_field = driver.find_element(By.CLASS_NAME, 'bf-upload-file-input')
upload_field.send_keys(file)
```
```

</div>