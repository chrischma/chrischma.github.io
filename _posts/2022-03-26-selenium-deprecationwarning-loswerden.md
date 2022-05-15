---
id: 285
title: 'Selenium – DeprecationWarning loswerden'
date: '2022-03-26T09:36:04+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=285'
permalink: /2022/03/26/selenium-deprecationwarning-loswerden/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2022/03/Thumbnail-deprecation.jpg'
categories:
    - 'Bots und Automatisierung'
    - Selenium
---

Hallo und ganz herzlich willkommen zurück. Heute wollen wir uns mal einer kleinen aber nervigen Fehlermeldung widmen, der ihr bestimmt schon mal begegnet seid: Und zwar ist das die DeprecationWarning.

Was genau das ist, wieso das Problem entsteht und wie man es lösen kann, das erfahrt ihr jetzt. Viel Spaß!

<figure class="wp-block-embed is-type-video is-provider-youtube wp-block-embed-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" frameborder="0" height="387" loading="lazy" src="https://www.youtube.com/embed/2Curetsnbmo?feature=oembed" title="Deprecation Warning loswerden ⚠️ (Python Selenium) | Tutorial für Anfänger | Deutsch" width="688"></iframe></div></figure>## So entsteht eine DeprecationWarning

Ich hab hier mal ein einfaches Beispielskript angelegt. Das Skript geht einfach auf die Website eine Bibliothek und tippt einen Suchbegriff in ein Suchfeld ein.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```

from selenium import webdriver

driver = webdriver.Chrome()

# Website aufrufen
driver.get('https://www.ub.uni-leipzig.de/start/')

# Suchfeld ausfüllen
search_field = driver.find_element_by_id('searchForm_lookfor')
search_field.send_keys('Mein cooler Suchbegriff')
```
```

</div>So weit funktioniert das auch alles ganz gut. Wenn ich das Skript ausführe, kriege ich allerdings hier immer die besagte Fehlermeldung. Und der erste Schritt, um einen Fehler loszuwerden, ist natürlich, den Fehler aufmerksam zu lesen. Das ist, gerade wenn man kürzlich mit Programmieren angefangen hat, ziemlich lästig, lohnt sich allerdings immer. Denn meistens finden sich alle wichtigen Details, die wir benötigen, um den Fehler zu beseitigen direkt in der Meldung.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
/Users/Chris/warning.py:10: DeprecationWarning: find_element_by_* commands are deprecated. Please use find_element() instead
```
```

</div>Was bedeutet das nun? Wir haben offensichtlich einen Fehler in Zeile 10. Und das ist die Zeile, in der wir nach unserem Suchfeld suchen. DeprecationWarning lässt sich leider relativ schlecht übersetzen, bedeutet aber so viel wie dass ein bestimmter Befehl veraltet ist und entsprechend zukünftig nicht mehr verwendet werden sollte. Und dieser veraltete Befehl ist die Funktion „find\_element\_by\_id“. Man findet blöderweise diesen Befehle immer noch in den allermeisten Tutorials und auch ich finde den Befehl irgendwie ziemlich intuitiv und benutze ihn deshalb gern. Trotzdem gibt’s dafür inzwischen eine neue Funktion, die wir jetzt mal brav in unser Skript einbauen. Und wenn alles gut geht, sollte dann kein Fehler mehr auftauchen.

## So lässt sich die DeprecationWaring vermeiden

Unser Code braucht eigentlich nur zwei kleine Veränderungen, um nicht mehr von der Fehlermeldung betroffen zu sein. Es gibt bei Selenium eine Klasse, die statt des Befehls „find\_element\_by\_id“ verwendet werden sollte. Und die nennt sich einfach ‚By‘. Um die nutzen zu können, importiere ich die jetzt direkt mal.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from selenium import webdriver
from selenium.webdriver.common.by import By
```
```

</div>Okay. Importiert haben wir die Klasse jetzt – und jetzt muss ich eigentlich nur noch meinen Befehl in Zeile 10 anpassen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
search_field = driver.find_element(By.ID, 'searchForm_lookfor')
```
```

</div>Und wenn ich jetzt mein Skript ausführe, sollte alles wieder butterweich und vor allem ohne Fehlermeldung laufen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()

# Website aufrufen
driver.get('https://www.ub.uni-leipzig.de/start/')

# Suchfeld ausfüllen
search_field = driver.find_element(By.ID, 'searchForm_lookfor')
search_field.send_keys('Mein cooler Suchbegriff')
```
```

</div>