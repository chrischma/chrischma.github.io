---
id: 352
title: 'Nachrichten mit Python an Discord schicken'
date: '2022-04-20T18:40:57+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=352'
permalink: /2022/04/20/nachrichten-mit-python-an-discord-schicken/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Discord-Thumbnail.png'
categories:
    - Discord
---

<figure class="wp-block-image size-large">![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Discord-Thumbnail-1-1024x676.png)</figure>Neulich hab ich mir aus Interesse mal angeschaut, wie man eigentlich mit Python Nachrichten an Discord schicken kann. Und weil ich danach total begeistert war wie einfach das geht, wie ist es heute mal mit euch teilen. Wichtig ist, dass ihr für dieses Video schon Python installiert habt, falls ihr dabei allerdings noch Unterstützung brauchen sollte, verlink ich euch aber in der Beschreibung noch ein Video, wo ich das nochmal ausführlich erkläre. Dort findet ihr auch wie immer die Timecodes, den Quellcode und einen passenden Artikel zu diesem Video.

## Requests installieren

Für unser kleines Programm brauchen wir das Modul requests. Das hilft uns dann, mit dem Server von Discord zu kommunizieren. Wahrscheinlich habt ihr das Modul eh schon installiert, sollte das allerdings nicht der Fall sein, dann ist das auch schnell erledigt. Dafür macht ihr einfach euer Terminal auf bzw. die Eingabeaufforderung auf Windows und tippt dort dann ein pip3 install requests. Und wenn das erledigt ist haben wir auch schon alles installiert, was wir brauchen.

Jetzt können wir requests auch schon importieren. Genauer gesagt wollen wir aus dem Modul requests einen kleinen Teil importieren. Der nennt sich post und ermöglicht es uns, Anfragen an Server zu schicken. Das Modul ist jetzt importiert und ab sofort können wir Anfragen an den Discord-Server senden.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from requests import post
```
```

</div>## Discord vorbereiten

Im Moment weiß der Discord-Server noch nichts von seinem Glück, dass wir ihm gleich eine Nachricht schicken werden. Damit Discord Bescheid weiß, müssen wir einen Webhook einrichten. Und das klingt komplizierter als es eigentlich ist. Denn so ein Webhook ist nichts anderes als eine Art Tunnel, über den unsere Nachricht zu Discord gelangt.

Dafür mache ich Discord auf, klicke dann auf den Server, mit dem ich interagieren möchte, klicke auf den Pfeil nach unten und wähle „Servereinstellungen.“

<figure class="wp-block-image size-large">![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Bildschirmfoto-2022-04-20-um-20.22.04-1024x497.png)</figure>Hier gehe ich jetzt auf Integrationen -&gt; Webhooks und dann auf Neuer WebHook.

<figure class="wp-block-image size-large">![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Bildschirmfoto-2022-04-20-um-20.23.17-1024x598.png)</figure>Meinem Webhook gebe ich als nächstes einen Namen. Ich nenne den jetzt einfach MeinWebhook. Den Namen werden wir gleich noch brauchen und genau deshalb nehm ich den gleich mal mit in mein Skript.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
username = 'MeinWebhook'
```
```

</div>Außerdem wähle ich hier jetzt noch den Kanal aus, in den ich denn schreiben möchte. In meinem Fall ist das jetzt mal Testweise der Kanal „Eure Projekte“.

Damit ist unser Webhook jetzt auch schon eingerichtet. Wir müssen uns jetzt nur noch die Internetadresse kopieren, unter der der WebHook erreichbar ist. Und dafür klicke ich einfach auf „WebHook-URL kopieren“. Und genau wie den Namen speichere ich mir die URL gleich mal in einer Variable.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
webhook_url = 'https://discord.com/api/webhooks/966397654806442044/I65A17tV9JGY9eI8kAKCTrD_I-J547Bk5wEIwI1C8nDljHhrZGOsB3LYh700OC_oqprd'
```
```

</div>## Senden-Funktion schreiben

Die Verbindung zum Server steht schon mal und deshalb ist es höchste Zeit, dass wir unsere Nachricht vorbereiten. Dafür schreiben wir jetzt einmal eine kleine Funktion, die wir dann später beliebig oft und mit beliebigen Textnachrichten wiederverwenden können. Meine Funktion nenne ich passenderweise send\_to\_discord.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def send_to_discord(content):
```
```

</div>Zu der Funktion gehören noch ein paar Daten, die Discord brauch, um unsere Anfrage zu verstehen. Und die legen wir jetzt einmalig fest.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
def send_to_discord(content):
	
	data = {                 
		"content": content,     # Den Content geben wir der Funktion mit...
		"username": username    # ... und den Username haben wir eh schon hinterlegt... ;-)
	}
```
```

</div>Und jetzt können wir den ganzen Bumms auch schon an Discord schicken. Dafür rufen wir die post-Methode auf. Und der geben wir zwei Sachen mit, nämlich unsere WebHook-URL, damit klar ist wo die Anfrage hingeschickt werden soll. Und wir geben natürlich die Daten mit, die wir gerade festgelegt haben, also den Text, den wir senden wollen und natürlich den Nutzernamen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
post(webhook_url, data=data)
```
```

</div>## Skript ausführen

Die Funktion ist fertig und wir können die jetzt ganz beliebig verwenden. Testweise können wir jetzt ja mal versuchen, Discord einfach freundlich zu grüßen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
send_to_discord('Hallo Discord!')
```
```

</div><div class="hcb_wrap">```
<pre class="prism line-numbers lang-bash" data-lang="Bash">```
Skript ausführen: 
Chris@MacBook-Air ~ % python3 send_to_discord.py
```
```

</div><figure class="wp-block-image size-large">![](https://christoph-schmalfuss.de/blog/wp-content/uploads/2022/04/Bildschirmfoto-2022-04-20-um-20.38.22-1024x250.png)</figure>Das funktioniert wunderbar – so einfach ist es also, mit Python Nachrichten in einen Discord-Channel zu schicken. Ich hoffe das Video war für euch nützlich, ich wünsch euch jetzt noch eine wunderbare Woche, bleibt neugierig und bis bald!