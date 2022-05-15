---
id: 310
title: 'Python Selenium wait &#8211; Warten, bis Bedingung erfüllt ist'
date: '2022-04-02T18:51:19+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=310'
permalink: /2022/04/02/python-selenium-wait-warten-bis-elemente-da-sind/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Thumbnail-wait.png'
categories:
    - 'Bots und Automatisierung'
    - Selenium
tags:
    - Bot
    - Python
---

<figure class="wp-block-image size-large">![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Thumbnail-wait-1024x576.png)</figure>Manchmal kann es notwendig sein, dass wir nicht sofort mit Elementen interagieren, sondern erstmal auf die Elemente warten. Das kann z.B. der Fall sein, wenn eine Seite langsam lädt, wenn wir uns zuerst einloggen müssen oder wenn ein langer Ladebalken gefüllt sein muss, bevor es weitergeht.

Selenium bietet da aber glücklicherweise eine Menge nützlicher Funktionen, die genau für solche Situationen nutzen können. Wie die funktionieren, schauen wir uns am besten direkt mal an einem einfachen Beispiel an.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()
driver.get('https://wikipedia.de')

# Hier soll gewartet werden...

search_bar = driver.find_element(By.ID, 'txtSearch')
search_bar.send_keys('Europa')
```
```

</div>Um Selenium jetzt vor der Eingabe auf das Element warten zu lassen, müssen wir zunächst zwei neue Sachen importieren. Zuerst brauchen wir die Klasse *WebDriverWait*. Mit der können wir Selenium dann zwingen, auf Elemente zu warten.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from selenium.webdriver.support.ui import WebDriverWait
```
```

</div>Außerdem brauchen wir die sogenannten expected\_condition. Und das sind einfach die Bedingungen, auf die wir warten. Das kann dann also z.B. sein, dass ein bestimmter Button nicht mehr ausgegraut ist oder das ein Element sichtbar ist.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from selenium.webdriver.support import expected_conditions as EC
```
```

</div>Jetzt stehen uns also verschiedene Bedingungen zur Verfügung. Und welche genau wir verwenden, legen wir jetzt fest.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
expected_condition = EC.visibility_of_element_located((By.ID, 'txtSearch'))
```
```

</div>Als nächstes befehlen wir unserem Webdriver zu warten. Dafür brauchen wir erstmal die Variable `wait`.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
wait = WebDriverWait(driver, 1000)
```
```

</div>Und jetzt müssen wir die Befehle nur noch verknüpfen. Wir sagen also Selenium jetzt einfach: Warte jetzt so lange, bis die Bedingung erfüllt ist, die ich festgelegt hab.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
wait.until(expected_condition)
```
```

</div>Und damit ist unser Skript jetzt auch schon startklar. Und um den Effekt mal ganz krass sichtbar zu machen, lösch ich jetzt noch die Zeile raus, wo wir Selenium sagen, auf welche Website navigiert werden soll. Und erst wenn ich dann wirklich die Website aufrufe, soll es weitergehen. Wenn alles glatt gegangen ist, wird Selenium jetzt also erst zu tippen anfangen, wenn die Suchleiste wirklich geladen ist.

### ✅ Kompletter Quellcode

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
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
```

</div>Und damit haben wir’s auch schon geschafft: So einfach ist es also, Selenium zu befehlen, auf bestimmte Sachen zu warten. Es gibt natürlich noch viel mehr Bedingungen als ob z.B. ein Element sichbar ist. [Eine komplette Liste der Bedingungen verlinke ich euch unten in der Kommentarspalte](https://www.selenium.dev/selenium/docs/api/py/webdriver_support/selenium.webdriver.support.expected_conditions.html). Es lohnt sich auf jeden Fall, da einfach mal ein bisschen auf Entdeckungsreise zu gehen. Ich zumindest bin immer wieder überrascht, was Selenium alles kann.

Für heute war’s das aber erstmal. Ich wünsch euch jetzt noch eine wunderbare Woche, bleibt neugierig und bis bald!