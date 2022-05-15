---
id: 145
title: 'Krypto-Kurse tracken mit Python'
date: '2021-10-29T12:00:00+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=145'
permalink: /2021/10/29/krypto-kurse-tracken-mit-python/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/10/Thumbnail-bitcoin.jpg'
categories:
    - API
    - 'Bots und Automatisierung'
tags:
    - Aktien
    - API
    - Bitcoin
    - Crypto
    - Etherium
    - Krypto
    - Request
    - Tracking
    - Währungen
---

Heute schreiben wir ein einfaches Python-Skript, mit dem wir den Kurs von beliebigen Kryptowährungen beobachten können. Das Skript wird aller paar Sekunden nach dem aktuellen Kurs schauen. Und sobald der Kurs einen bestimmten Wert übersteigt, werden wir benachrichtigt. Schauen wir uns an, wie’s funktioniert

## Unsere Datenquelle

Unsere Daten können wir aus verschiedenen Quellen beziehen. Wir nutzen für unser Skript [coinapi.io](https://www.coinapi.io). Dort kann man sich kostenlos anmelden und hat dann Zugriff auf allerhand nützliche Daten.

Sobald wir uns angemeldet haben, wird uns ein eigener API-Key per E-Mail zugeschickt. Und der ermöglicht es uns, dass Python mit coinapi.io kann.

## Eine API-Anfrage stellen

Wir können mit unserem API-Key nun Anfragen an coinapi stellen. Dafür nutzen wir das Modul requests. Das können wir bequem über das Terminal installieren.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
pip3 install requests
```
```

</div>Alles, was wir über die API von coinapi.io wissen müssen, finden wir in deren [Dokumentation](https://docs.coinapi.io/#md-docs). Aus dieser Dokumentation suchen wir nun die passende Anfrage heraus. Ich zeig euch hier mal exemplarisch wie ihr den Bitcoin-Kurs in USD auslesen könnt, das funktioniert aber mit jeder beliebigen Krypowährung genaus so.

In unserem Fall wollen wir also auf die Markt-Daten zugreifen, genauer gesagt auf einen bestimmten Wechselkurs. Deshalb wähle ich aus den Market-Data den Bereich [Get spefic rate](https://docs.coinapi.io/?python#get-specific-rate-get) aus.

<figure class="wp-block-image size-full">![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2021/10/Bildschirmfoto-2021-10-21-um-18.43.08.png)<figcaption>Die Dokumentation enthält bereits eine passende Anfrage.</figcaption></figure>Oben rechts kann ich mir den entsprechenden Quellcode in verschiedenen Programmiersprachen anzeigen lassen. Ich schnappe mir den Python-Code und nehme ihn mit in mein Skript.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import requests # das Skript wird importiert
url = 'https://rest.coinapi.io/v1/exchangerate/BTC/USD' # diese URL wird bei der Anfrage aufgerufen
headers = {'X-CoinAPI-Key' : '73034021-THIS-IS-SAMPLE-KEY'} # unser API-Key wird mitgegeben
response = requests.get(url, headers=headers) # wird starten die Anfrage
```
```

</div>Der API-Key stimmt jetzt natürlich noch nicht. Deshalb füge ich meinen persönlichen Key jetzt in das Skript ein. Den habe ich ja bereits per E-Mail bekommen.

Das sollte jetzt auch schon funktionieren. Um herauszufinden, was uns für Daten zurückgegeben werden, lass ich mir die entsprechende Antwort ausgeben.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
print(response.text)
```
```

</div>Aus der Antwort interessiert uns jetzt eigentlich nur ein Wert, und zwar der aktuelle Kurs. Und genau den lesen wir nun aus.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
current_rate = response.json()['rate']
print(current_rate)
```
```

</div>Und damit haben wir jetzt schon unsere erste Funktion. Ich gebe meiner Funktion einen Namen und rücke den Quellcode ein, sodass er in der Funktion hinterlegt ist. Und ganz am Ende der Funktion lasse ich mir den Wert mit dem Schlüsselwort `return` zurückgeben.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def get_current_rate():
    url = 'https://rest.coinapi.io/v1/exchangerate/BTC/USD'
    headers = {'X-CoinAPI-Key' : 'yyyyyyxxxxxxxxyyyyyyyyxxxxx'
    response = requests.get(url, headers=headers)
    
    current_rate = response.json()['rate']
    return current_rate
```
```

</div>## Bitcoin-Kurs tracken

Als nächstes wollen wir den Kurs vergleichen und benachrichtigt werden, wenn der Kurs eine bestimmte Marke übersteigt. Auch das tun wir in einer eigenen Funktion. Den Zielwert, auf den wir warten wollen, hinterlegen wir gleich mal in einer eigenen Variable. Und sobald dieser Zielerwert erreicht wird, wollen wir dann benachrichtigt werden.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
goal_rate = 65000
```
```

</div><div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def compare_current_rate_with_goal():
    current_rate = get_current_rate()

    if current_rate >= goal_rate:
        notify_user()

    print(f'Aktueller Kurs: {round(current_rate)} USD')
```
```

</div>## Eine Benachrichtigung einrichten

Die Benachrichtigung des Nutzers kann jetzt auf ganz viele verschiedene Weisen erfolgen. Ich kann mir z.B. Benachrichtigungen per Mail oder per Telegram schicken lassen. Entsprechende Tutorials dazu verlinke ich euch in der Videobeschreibung. Wir machen das jetzt aber mal etwas einfacher. Und zwar soll einfach ein Soundeffekt abgespielt werden und eine Nachricht im Terminal angezeigt werden.

Zum Abspielen von Sounds können wir das Modul *simpleaudio* verwenden. Das funktioniert auf allen Plattformen und ist ziemlich einfach zu bedienen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
pip3 install simpleaudio
```
```

</div><div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import simpleaudio
```
```

</div>Wo wir den Soundeffekt jetzt hernehmen, ist im Prinzip egal. Es gibt online ja eine Menge kostenloser Quellen für Soundeffekte, die wir für solche Projekte nutzen können. Oder ihr macht es wie ich und nervt eure Freundin so lange, bis sie mit euch gemeinsam eine kleine Aufnahmesession macht. Wir haben uns dafür einfach ein Glas geschnappt und ein paar Münzen reingeschmissen. Das Ganze habe wir einfach mit meinem China-Handy aufgenommen und schon hatten wir einen hübschen und vor allem copyrightfreien Soundeffekt.

Den aufgenommenen Soundeffekt nehme ich dann und lege ihn in meinem Projektordner ab. Das mache ich idealerweise in einem Unterordner, damit das Projekt übersichtlich bleibt.

Anschließend lege ich die Funktion an, die den Nutzer benachrichtigt und den Soundeffekt abspielt.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def notify_user():
    print(f'Der Kurs hat die Zielmarke von {goal_rate} USD erreicht!')

    wave_object = simpleaudio.WaveObject.from_wave_file('./sounds/coins.wav')
    play_object = wave_object.play()
    play_object.wait_done()
    exit()

```
```

</div>## Funktion in Schleife ausführen

Unser Programm hat jetzt an sich alles was es braucht. Als letztes basteln wir jetzt noch eine kleine Schleife, die sich auf die Lauer legt und regelmäßig für uns den Kurs checkt. Dafür importieren wir uns die Funktion time.sleep().

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from time import sleep
```
```

</div>Und mit der schreiben wir jetzt eine Schleife, die z.B. aller 5 Sekunden den Kurs checkt.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def track_rate():

    while True:
        print('\nTracke Bitcoin-Kurs...')
        compare_current_rate_with_goal()
        sleep(5)
```
```

</div>Wichtig ist hier allerdings zu wissen, dass wir pro Tag 100 API-Anfragen kostenlos stellen können. Deshalb ist es empfehlenswert, in unsere Sleepfunktion eine wesentlich größere Sekundenanzahl anzugeben. Für jetzt ist 5 Sekunden aber erstmal okay – so könnt ihr gut sehen, wie das Programm arbeitet.

Und zu guter Letzt legen wir jetzt noch fest, dass diese Funktion immer aufgerufen werden soll, wenn wir das Skript direkt aufrufen. Dafür nutzen wir die if \_\_name\_\_ == „\_\_main\_\_“ Funktion.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
if __name__ == "__main__":
    track_rate()
```
```

</div>Und damit haben wir es geschafft.

## ✅ Kompletter Quellcode

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
import requests
import simpleaudio
from time import sleep


goal_rate = 65000


def get_current_rate():
    url = 'https://rest.coinapi.io/v1/exchangerate/BTC/USD'
    headers = {'X-CoinAPI-Key' : '_____________________________'}
    response = requests.get(url, headers=headers)

    current_rate = response.json()['rate']
    return current_rate


def notify_user():
    print(f'Der Kurs hat die Zielmarke von {goal_rate} USD erreicht!')

    wave_object = simpleaudio.WaveObject.from_wave_file('./sounds/coins.wav')
    play_object = wave_object.play()
    play_object.wait_done()

    exit()


def compare_current_rate_with_goal():
    current_rate = get_current_rate()

    if current_rate >= goal_rate:
        notify_user()

    print(f'Aktueller Kurs: {round(current_rate)} USD')


def track_rate():

    while True:
        print('\nTracke Bitcoin-Kurs...')
        compare_current_rate_with_goal()
        sleep(3)


if __name__ == "__main__":
    track_rate()

```
```

</div>