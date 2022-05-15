![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/03/Thumbnail-deprecation-1600x900.jpg)

Selenium – DeprecationWarning loswerden
=======================================

Hallo und ganz herzlich willkommen zurück. Heute wollen wir uns mal einer kleinen aber nervigen Fehlermeldung widmen, der ihr bestimmt schon mal begegnet seid: Und zwar ist das die DeprecationWarning.

Was genau das ist, wieso das Problem entsteht und wie man es lösen kann, das erfahrt ihr jetzt. Viel Spaß!

So entsteht eine DeprecationWarning
-----------------------------------

Ich hab hier mal ein einfaches Beispielskript angelegt. Das Skript geht einfach auf die Website eine Bibliothek und tippt einen Suchbegriff in ein Suchfeld ein.

```python
from selenium import webdriver

driver = webdriver.Chrome()

# Website aufrufen
driver.get('https://www.ub.uni-leipzig.de/start/')

# Suchfeld ausfüllen
search_field = driver.find_element_by_id('searchForm_lookfor')
search_field.send_keys('Mein cooler Suchbegriff')
```

So weit funktioniert das auch alles ganz gut. Wenn ich das Skript ausführe, kriege ich allerdings hier immer die besagte Fehlermeldung. Und der erste Schritt, um einen Fehler loszuwerden, ist natürlich, den Fehler aufmerksam zu lesen. Das ist, gerade wenn man kürzlich mit Programmieren angefangen hat, ziemlich lästig, lohnt sich allerdings immer. Denn meistens finden sich alle wichtigen Details, die wir benötigen, um den Fehler zu beseitigen direkt in der Meldung.

```python
/Users/Chris/warning.py:10: DeprecationWarning: find_element_by_* commands are deprecated. Please use find_element() instead
```

Was bedeutet das nun? Wir haben offensichtlich einen Fehler in Zeile 10. Und das ist die Zeile, in der wir nach unserem Suchfeld suchen. DeprecationWarning lässt sich leider relativ schlecht übersetzen, bedeutet aber so viel wie dass ein bestimmter Befehl veraltet ist und entsprechend zukünftig nicht mehr verwendet werden sollte. Und dieser veraltete Befehl ist die Funktion „find\_element\_by\_id“. Man findet blöderweise diesen Befehle immer noch in den allermeisten Tutorials und auch ich finde den Befehl irgendwie ziemlich intuitiv und benutze ihn deshalb gern. Trotzdem gibt’s dafür inzwischen eine neue Funktion, die wir jetzt mal brav in unser Skript einbauen. Und wenn alles gut geht, sollte dann kein Fehler mehr auftauchen. 

So lässt sich die DeprecationWaring vermeiden
---------------------------------------------

Unser Code braucht eigentlich nur zwei kleine Veränderungen, um nicht mehr von der Fehlermeldung betroffen zu sein. Es gibt bei Selenium eine Klasse, die statt des Befehls „find\_element\_by\_id“ verwendet werden sollte. Und die nennt sich einfach ‚By‘. Um die nutzen zu können, importiere ich die jetzt direkt mal.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
```

Okay. Importiert haben wir die Klasse jetzt – und jetzt muss ich eigentlich nur noch meinen Befehl in Zeile 10 anpassen. 

```python
search_field = driver.find_element(By.ID, 'searchForm_lookfor')
```

Und wenn ich jetzt mein Skript ausführe, sollte alles wieder butterweich und vor allem ohne Fehlermeldung laufen.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()

# Website aufrufen
driver.get('https://www.ub.uni-leipzig.de/start/')

# Suchfeld ausfüllen
search_field = driver.find_element(By.ID, 'searchForm_lookfor')
search_field.send_keys('Mein cooler Suchbegriff')
```

![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Thumbnail-wait.png)

Python Selenium wait – Warten, bis Bedingung erfüllt ist
========================================================

![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Thumbnail-wait-1024x576.png)
Manchmal kann es notwendig sein, dass wir nicht sofort mit Elementen interagieren, sondern erstmal auf die Elemente warten. Das kann z.B. der Fall sein, wenn eine Seite langsam lädt, wenn wir uns zuerst einloggen müssen oder wenn ein langer Ladebalken gefüllt sein muss, bevor es weitergeht.

Selenium bietet da aber glücklicherweise eine Menge nützlicher Funktionen, die genau für solche Situationen nutzen können. Wie die funktionieren, schauen wir uns am besten direkt mal an einem einfachen Beispiel an.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()
driver.get('https://wikipedia.de')

# Hier soll gewartet werden...

search_bar = driver.find_element(By.ID, 'txtSearch')
search_bar.send_keys('Europa')
```

Um Selenium jetzt vor der Eingabe auf das Element warten zu lassen, müssen wir zunächst zwei neue Sachen importieren. Zuerst brauchen wir die Klasse *WebDriverWait*. Mit der können wir Selenium dann zwingen, auf Elemente zu warten.

```python
from selenium.webdriver.support.ui import WebDriverWait
```

Außerdem brauchen wir die sogenannten expected\_condition. Und das sind einfach die Bedingungen, auf die wir warten. Das kann dann also z.B. sein, dass ein bestimmter Button nicht mehr ausgegraut ist oder das ein Element sichtbar ist.

```python
from selenium.webdriver.support import expected_conditions as EC
```

Jetzt stehen uns also verschiedene Bedingungen zur Verfügung. Und welche genau wir verwenden, legen wir jetzt fest.

```python
expected_condition = EC.visibility_of_element_located((By.ID, 'txtSearch'))
```

Als nächstes befehlen wir unserem Webdriver zu warten. Dafür brauchen wir erstmal die Variable `wait`. 

```python
wait = WebDriverWait(driver, 1000)
```

Und jetzt müssen wir die Befehle nur noch verknüpfen. Wir sagen also Selenium jetzt einfach: Warte jetzt so lange, bis die Bedingung erfüllt ist, die ich festgelegt hab.

```python
wait.until(expected_condition)
```

Und damit ist unser Skript jetzt auch schon startklar. Und um den Effekt mal ganz krass sichtbar zu machen, lösch ich jetzt noch die Zeile raus, wo wir Selenium sagen, auf welche Website navigiert werden soll. Und erst wenn ich dann wirklich die Website aufrufe, soll es weitergehen. Wenn alles glatt gegangen ist, wird Selenium jetzt also erst zu tippen anfangen, wenn die Suchleiste wirklich geladen ist.

### ✅ Kompletter Quellcode

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()

expected_condition = EC.visibility_of_element_located((By.ID, 'txtSearch'))
wait = WebDriverWait(driver, 1000)
wait.until(expected_condition)

search_bar = driver.find_element(By.ID, 'txtSearch')
search_bar.send_keys('Europa')
```

Und damit haben wir’s auch schon geschafft: So einfach ist es also, Selenium zu befehlen, auf bestimmte Sachen zu warten. Es gibt natürlich noch viel mehr Bedingungen als ob z.B. ein Element sichbar ist. [Eine komplette Liste der Bedingungen verlinke ich euch unten in der Kommentarspalte](https://www.selenium.dev/selenium/docs/api/py/webdriver_support/selenium.webdriver.support.expected_conditions.html). Es lohnt sich auf jeden Fall, da einfach mal ein bisschen auf Entdeckungsreise zu gehen. Ich zumindest bin immer wieder überrascht, was Selenium alles kann. 

Für heute war’s das aber erstmal. Ich wünsch euch jetzt noch eine wunderbare Woche, bleibt neugierig und bis bald!

![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Thumbnail-selenium-login-1600x1600.png)

Eingeloggt bleiben – Python Selenium | Login dauerhaft speichern
================================================================

Das ständige Einloggen auf Websites kann beim Automatisieren und beim Webscraping viel Zeit und nerven kosten. Deshalb schauen wir uns heute mal an, wie man so einen Login speichern und überspringen kann. Und um eine Frage gleich mal vorweg zu beantworten: Ja, das Prinzip funktioniert auf fast allen Websites. Viel Freude mit dem Video, los geht’s!

![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Thumbnail-selenium-login-1024x1024.png)
Vorbereitung – Module importieren

---------------------------------

So ein Login funktioniert eigentlich immer gleich. Wir gehen auf eine Website, geben unsere Daten ein und dann wird unser Login einem entsprechenden Cookie gespeichert. Und wenn wir den Cookie erstmal gespeichert haben, bleibt der in der Regel mehrere Jahre gültig, sodass wir uns zukünftig nicht mehr einloggen müssen, sondern einfach den Cookie laden, den wir einmalig gespeichert haben. Und genau das ist auch das, was wir jetzt als erstes machen. 

Um das ganze mit Python umzusetzen, verwenden wir natürlich Selenium, damit wir unseren Browser fernsteuern können. Und da unsere Cookies im JSON-Format gespeichert werden, brauchen wir außerdem das Modul json. Wie genau das JSON-Format funktioniert, müsst ihr an dieser Stelle gar nicht wissen – ich verlink euch für den Fall der Fälle trotzdem unten in der Videobeschreibung ein Video, das das Ganze bisschen genauer erklärt.

```python
from selenium import webdriver
import json
```

Plattform festlegen
-------------------

Zunächst müssen wir natürlich die Cookies speichern, um sie später laden zu können. Dafür leg ich direkt mal fest, in welcher **Datei** meine Cookies eigentlich gespeichert werden sollen. 

Außerdem lege ich eine **Start URL** fest. Das ist die Internetseite, auf der ich später Anfangen will, mit Selenium zu surfen. Üblicherweise ist das einfach die Startseite der jeweiligen Plattform. Ich zeig euch das heute am Beispiel Twitter, deshalb lege ich als Start-URL die Startseite von Twitter fest. Wenn ihr das gleich für eine andere Website machen wollt, schreibt ihr also diese Website hier einfach rein. 

Und zu guter letzt legen wir auch gleich unseren Webdriver an, um dann den Browser fernzusteuern.

```python
cookies_file = 'twitter-cookies.json'
start_url = 'https://www.twitter.com'
driver = webdriver.Chrome()
```

Cookies speichern
-----------------

Für das Speichern der Cookies brauchen wir natürlich erstmal eine Funktion, die das für uns erledigt. Und der Funktion übergeben wir dann unseren Webdriver, den wir gerade benutzen. Der wird dann wie immer einfach driver heißen, deshalb schreibe ich in die Klammern „driver“.

```python
def save_cookies(driver):
```

Der Webdriver soll dann als erstes mal auf unsere Startseite gehen, damit wir uns bequem einloggen können. Und das machen wir mit der Funktion driver.get()

```python
def save_cookies(driver):
    driver.get(start_url)
```

Anschließend soll der Driver warten, bis wir uns eingeloggt haben und erst dann die Cookies abspeichern. Und das lösen wir hier so, dass der User einfach Enter drücken soll, sobald er fertig mit einloggen ist – und erst dann werden die Cookies gespeichert.

```python
    input('Press RETURN to save cookies!')
```

Und jetzt wird unser Skript also so lange nichts machen, bis wir Enter gedrückt haben. 

Als nächstes legen wir fest, was passieren soll, nachdem wir Enter gedrückt haben. Dann sollen ja die Cookies vom Webdriver ausgelesen werden und dafür gibt es die Funktion get\_cookies()

```python
    cookies = driver.get_cookies()
```

Jetzt sind die Cookies ausgelesen. Blöderweise werden uns die Daten allerdings als Python Objekt und nicht als JSON zurückgegeben, deshalb machen wir aus dem Python Objekt jetzt einen schönen JSON string.

```python
    cookies = json.dumps(cookies)
```

Um später auf die Cookies zugreifen zu können, speichern wir die Cookies in einer Datei. 

```python
    with open(cookies_file, 'w') as f:
        f.write(cookies)
```

Und wenn wir fertig sind mit dem ganzen Bumms, dann schließen wir einfach unseren Browser.

```python
driver.quit()
```

Unsere Funktion ist fertig und kann jetzt auch schon ausgeführt werden. Dafür rufe ich die Funktion einfach auf.

```python
save_cookies(driver)
```

```python
Nachdem wir das Skript aufgerufen haben, speichert Python alle wichtigen Daten in unserer .json-Datei. 

[{"domain": ".twitter.com", "expiry": 165088791156, "httpOnly": true, ...
```

Cookies laden
-------------

Der Login ist jetzt in unserer JSON-Datei gespeichert. Und anstatt uns zukünftig immer einzuloggen, schreiben wir jetzt eine Funktion, die automatisch den vorhanden Login-Cookie aus unserer Datei lädt und so den Login überspringt.

Dazu öffnen wir zu allererst die Datei und holen uns die Daten heraus.

```python
def load_cookies(driver):
    with open(cookies_file, 'r') as f:
        cookies = json.load(f)
```

Anschließend wollen wir, dass unser Webdriver bequem direkt zur Startseite navigiert. 

```python
    driver.get(start_url)
```

Und wenn der Browser dann auf der Startseite angekommen ist, sollen alle Cookies zum aktuellen Webdriver hinzugefügt werden. Dafür bietet sich eine kleine for-Schleife an. Und die sorgt dafür, dass Python durch alle gespeicherten Cookies geht und sie dem Webdriver hinzufügt.

```python
    for cookie in cookies:
        driver.add_cookie(cookie)
```

Und wenn dann alle Cookies geladen sind, soll die Seite nochmal aktualisiert werden, damit wir nicht mehr die alte Seite sehen, sondern die Version der Seite, bei der wir schon eingeloggt sind. 

```python
    driver.refresh()
```

Und als letztes geben wir jetzt einfach den driver mitsamt Cookies wieder zurück, sodass wir mit dem driver dann eingeloggt alle anderen Dinge tun können, die wir so vorhaben.

```python
   return driver
```

Skript ausführen
----------------

Jetzt, da unsere Cookies schon gespeichert sind, brauchen wir die save Funktion nicht mehr. Ich lasse sie trotzdem noch gespeichert, falls wir sie später noch einmal brauchen, lösche aber die Zeile raus, in der die Funktion wirklich aufgerufen wird (`save_cookies(driver)`).

Stattdessen rufe ich jetzt die load\_cookies Funktion auf. Und das Ergebnis der Funktion, also meinen eingeloggten Webdriver, speichere ich mir direkt in der Variable `driver`, mit der ich dann beliebig eingeloggt weiterarbeiten kann. Und wenn ich das Skript jetzt ausführe, loggt sich der Browser für mich automatisch ein und mir bleibt für die nächsten Jahre erstmal das Einloggen erspart. 

```python
driver = load_cookies(driver)
```

Und so einfach ist es also, sich mit Selenium dauerhaft einzuloggen.

✅ Kompletter Quellcode
----------------------

```python
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

![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Thumbnail-Dateien-hochladen.png)

Python Selenium – Dateien automatisch hochladen
===============================================

![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Thumbnail-Dateien-hochladen-1024x576.png)
Hallo und herzlich willkommen zurück!

Heute wollen wir uns mal anschauen, wie man mit Python Dateien automatisiert auf Webseiten hochladen kann. Ich zeig euch das anhand der Website file-upload.net, das Prinzip das ihr gleich kennenlernt funktioniert aber genau so auch auf 99% der anderen Websites, die man so online finden kann. Den Quellcode, einen passenden Artikel und die Timecodes gibt’s wie immer in der Beschreibung, springt also gern zu den Teilen des Videos, die für euch interssant sind. Viel Freude!

Wie funktioniert ein Dateiupload?
---------------------------------

Wie immer schauen wir uns als erstes an, wie eigentlich der Prozess genau aussieht, den wir automatisieren wollen. Und um eine Datei auf einer Webseite hochzuladen, machen wir ja natürlich erstmal unseren Browser auf, gehen auf unsere Ziel-Webseite klicken dann auf einen Uploadbutton, wählen die Datei aus und bestätigen das. 

Das sind also erstmal die Schritte, die wir als Mensch durchführen würden. Und da können wir uns jetzt eigentlich direkt daran machen, die Schritte im Quellcode umzusetzen. 

Module importieren und Variablen festlegen
------------------------------------------

Als erstes importiere ich jetzt die Module, die wir heute brauchen. Einerseits ist natürlich der Selenium Webdriver, der für uns den Browser fernsteuert und andererseits brauchen wir noch die Klasse „By“, mit der wir Elemente auf der Website identifizieren können. 

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
```

Als nächstes legen wir fest, auf welcher Website wir unsere Datei hochladen und natürlich um welche Datei es eigentlich geht. 

```python
url = 'https://www.file-upload.net/'
file = '/Users/Chris/thumnail windows.jpg'
```

Website aufrufen
----------------

Nachdem geklärt ist, welche Website wir öffnen wollen, können wir unseren Webdriver jetzt auch schon losschicken. Dafür lege ich jetzt meinen Webdriver an…

```python
driver = webdriver.Chrome()
driver.get(url)
```

… und schicke ihn direkt auf die Website. 

Uploadfeld finden
-----------------

So ein Dateiupload geschieht in der Regel über ein Input Element. Das unterscheidet sich auch eigentlich nicht von anderen Eingabefeldern, außer dass es den Typ „File“ besitzt. Und genau danach können wir jetzt im Quellcode suchen.

![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Bildschirmfoto-2022-04-15-um-14.54.02-1024x615.png)
Dafür klicke ich einfach auf den Upload Bereich und suche dann nach einem Input Element, dass den Typ „File“ besitzt. 

```python
<input class="bf-upload-file-input" type="file" name="file" multiple="multiple">
```

An dieser Stelle vielleicht kleiner Hinweis: Auf manchen Websites, also z.B. beim Videoupload auf TikTok, ist das Input-Element versteckt, sodass wir damit nicht interagieren können. Sollte das der Fall sein, müssen wir das Element erst sichtbar machen, bevor wir damit Dateien hochladen können. Das ist aber unkompliziert, das entsprechende Video verlinke ich euch unten in der Videobeschreibung.

Uploadfeld Datei an das Uploadfeld schicken
-------------------------------------------

Mein Uploadfeld kenn ich jetzt, es wird also allerhöchste Zeit, dass wir unsere Datei an das Feld schicken. Und da gibt es eigentlich nur eine Sache, die man verstehen muss. Ich hab ja gerade schon erwähnt, dass so ein Datei-Uploader eigentlich nichts anderes ist als ein Eingabefeld. Und um etwas in ein Eingabefeld zu schreiben, kennen wir ja schon den Befehl send\_keys. 

Und genau weil ein Dateiupload eigentlich einfach ein Eingabefeld, ist können wir uns auch den ganzen Upload-Dialog sparen, sondern können den Link zur Datei auf unserem Computer einfach mit dem üblichen Befehl „send\_keys“ an das Feld schicken. Von unserem Dateiupload kennen wir ja zumindest den Namen der Klasse, und daran können wir das Feld jetzt auch eindeutig identifizieren.

```python
upload_field = driver.find_element(By.CLASS_NAME, 'bf-upload-file-input')
upload_field.send_keys(file)
```

Je nach Website müssen wir den Upload übrigens noch bestätigen und das würde mit folgendem Code funktionieren:

```python
upload_field.submit()
```

Und wenn wir das jetzt ausführen, sollte unsere Datei auch schon hochgeladen werden. Für unsere Website brauchen wir den Befehl nicht, aber ich wollte ihn euch zumindest zeigen, damit ihr die Lösung parat habt, falls sich bei eurem Dateiupload nichts tut.

Und damit haben wir’s auch schon geschafft – so einfach ist es also, Dateien mit Selenium auf Webseiten hochzuladen. Ich wünsch euch jetzt noch eine wunderbare Woche, bleibt neugierig und bis bald!

✅ Kompletter Quellcode
----------------------

```python
from selenium import webdriver
from selenium.webdriver.common.by import By


url = 'https://www.file-upload.net/'
file = '/Users/Chris/thumnail windows.jpg'

driver = webdriver.Chrome()
driver.get(url)

upload_field = driver.find_element(By.CLASS_NAME, 'bf-upload-file-input')
upload_field.send_keys(file)
```

![Das Bild zeigt ein Programmfenster, in welchem "Python Automatisierung" steht.](https://christoph-schmalfuss.de/blog/wp-content/uploads/2021/10/Thumbnail-automatisierung.png)

Tutorial: Automation mit Python
===============================

Immer wieder werde ich in den Kommentaren gefragt, wie man einen Browser fernsteuern kann. Und genau das lernen wir heute. Ich bin Chris – und das ist Programmieren mit Chris. Viel Spaß!

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

```python
import time  
from selenium import webdriver
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

[ausprobieren]

Okay, soviel erstmal für heute. Fragen und Wünsche könnt ihr wie immer in der Kommentarspalte dalassen, ich antworte bei passenden Fragen mit kurzen Videoantworten. Und jetzt viel Spaß beim Ausprobieren, bleibt neugierig und bis bald!

✅ Kompletter Quellcode
----------------------

```python
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
