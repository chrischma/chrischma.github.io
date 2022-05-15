---
id: 128
title: 'Python Telegram Bot &#8211; Nachrichten empfangen und beantworten 🤖'
date: '2021-10-22T14:00:17+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=128'
permalink: /2021/10/22/python-telegram-bot-nachrichten-empfangen-und-beantworten-%f0%9f%a4%96/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/10/Thumbnail-telegram-bot.jpg'
categories:
    - 'Bots und Automatisierung'
tags:
    - API
    - Bot
    - Python
    - Telegram
---

<figure class="wp-block-embed is-type-video is-provider-youtube wp-block-embed-youtube wp-embed-aspect-16-9 wp-has-aspect-ratio"><div class="wp-block-embed__wrapper"><iframe allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen="" frameborder="0" height="387" loading="lazy" src="https://www.youtube.com/embed/50XmGU5qSXs?feature=oembed" title="Python 🤖 Telegram Bot: Empfangen und Beantworten von Nachrichten | Tutorial für Anfänger" width="688"></iframe></div></figure>Heute schreiben wir einen einfachen Telegram-Bot, der Nachrichten empfangen und beantworten kann. Ich bin Chris und das ist Programmieren mit Chris. Viel Spaß!

Unser Bot soll am Ende wie folgt funktionieren. Er soll grundsätzlich erstmal auf Nachrichten warten und je nachdem, was wir ihm schreiben, unterschiedlich antworten. Wenn ich z.B. „hi“ schreibe, soll der Bot mir auch Hallo sagen. Und wenn ich etwas schreibe, was der Bot nicht erwartet hat, soll er auch eine passende Antwort parat haben.

Wir benutzen heute das Telegram-Bot-Modul. Das installieren wir ganz einfach mit folgendem Befehl:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
pip3 install python-telegram-bot
```
```

</div>Aus diesem Paket importieren wir uns jetzt Teil, den wir heute brauchen. Das ist der gesamte Bereich mit dem Namen telegram.ext und entsprechend schreiben wir folgenden Befehl:

## Vorbereitung

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from telegram.ext import * 
```
```

</div>Die Verknüpfung zwischen unserem Skript und Telegram passiert über eine API-Schnittstelle. Für die brauchen wir einen API Key. [Im ersten Video habe ich euch ja bereits gezeigt, wie ihr an einen solchen API-Code kommt. ](https://www.youtube.com/watch?v=DZP7MmhZ9IA&t=230s)

Ich zeig euch das trotzdem nochmal in Kurzform. Als erstes öffnen wir Telegram. Dort suchen wir dann nach dem BotFather.

<figure class="wp-block-image size-large">![Ein Chatfenster mit dem Botfather mit einer Begrüßungsnachricht.](https://christoph-schmalfuss.de/blog/wp-content/uploads/2021/10/Bildschirmfoto-2021-10-09-um-19.44.17-1024x661.png)<figcaption>So sieht die Begrüßung des BotFathers aus. </figcaption></figure>Danach klicke ich auf „Starten“ und gebe ein:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
/newbot
```
```

</div>Als erstes gebe ich meinem Bot einem Namen, z.B. Bernd Stromberg. Dann braucht mein Bot noch einen Usernamen, der mit \_bot endet. Ich nenne meinen Bot.

<figure class="wp-block-image">![]()</figure>Als Antwort erhalte ich jetzt einen API Key. Und den nehme ich gleich mal mit in mein Skript.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
API_KEY = '2089asdaa:AAEcadfasdfasdfasdfsYxrJv70UIQArs1YQ'
```
```

</div>## Nachrichten empfangen

Uns Skript braucht zuerst einmal einen Updater. Der Updater nimmt die Nachrichten, die wir dem Bot schreiben an. Und dann brauchen wir noch einen Dispatcher. Der kümmert sich sozusagen um die ganze Logistik, schickt also die Nachrichten über Telegram auf die Reise.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def main():
    updater = Updater(API_KEY)                                      # updater empfängt die Anfrage und gibt sie
    dp = updater.dispatcher    
```
```

</div>Damit unser Dispatcher Nachrichten entgegennehmen kann, müssen wir einen MessageHandler hinzufügen. Das geht folgendermaßen:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
    dp.add_handler(MessageHandler(Filters.text, handle_message))

    updater.start_polling(0)


```
```

</div>Die Funktion start\_polling sorgt einfach dafür, dass der Bot beginnt, auf Nachrichten zu warten. Der Filter bestimmt, auf welche Art von Inhalten der Bot später reagieren soll. Und handle\_message ist die Funktion, die wir aufrufen, sobald eine Nachricht eintrifft.

## Nachrichten beantworten

Immer wenn eine Nachricht jetzt beim Dispatcher eintrifft, gibt der Dispatcher zwei Informationen weiter. Einmal das Update selbst und dann noch dessen Context. Beide Informationen fangen wir mit unserer Funktion auf.

Wir lassen uns auch gleich mal das Update und den Context ausgeben.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def handle_message(update, context):                 
    print(update, context)
```
```

</div>Genau genommen kann unser Bot jetzt schon Nachrichten empfangen. Probieren wir das aus!

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
{'message': {'channel_chat_created': False, 'text': 'asdf', 'delete_chat_photo': False, 'new_chat_members': [], 'message_id': 31, 'new_chat_photo': [], 'date': 1633806064, 'caption_entities': [], 'entities': [], 'supergroup_chat_created': False, 'group_chat_created': False, 'photo': [], 'chat': {'type': 'private', 'first_name': 'Chris', 'username': 'christopf', 'id': 81102618}, 'from': {'first_name': 'Chris', 'username': 'christopf', 'is_bot': False, 'id': 81102618, 'language_code': 'de'}}, 'update_id': 920648929} <telegram.ext.callbackcontext.CallbackContext object at 0x10d7cfba0>
```
```

</div>Von den ganzen Daten, die unser Update enthält, brauchen wir ja eigentlich nur den Text. Genau deshalb holen wir uns den Text jetzt aus dem Update heraus.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
    text = update.message.text
```
```

</div>Und jetzt wo wir den Text haben, können wir eine Antwort generieren. Dafür erstelle ich jetzt eine neue Funktion, die die Nutzereingabe entgegennimmt und auf sie antwortet.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def create_responses(input_text):                  
    if input_text == "hi":
        return "Hey ho!"
    else:
        return 'Das habe ich nicht verstanden.'
```
```

</div>Die Funktion rufen wir jetzt immer auf, wenn ein Update reinkommt. Deshalb ergänzen wir jetzt noch einmal die handle\_message-Funktion.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
    response = create_responses(text)

```
```

</div>Und zu guter Letzt schicken wir die Antwort an den Nutzer aus.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
    update.message.reply_text(response)
```
```

</div>Unser Skript ist jetzt fast fertig. Wir müssen nur noch mit der *name equals main*-Funktion festlegen, dass unsere main-Funktion aufgerufen werden soll, sobald wir das Skript direkt starten.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
if __name__ == "__main__":
    main()

```
```

</div>Und damit haben wir es geschafft!

## ✅ Kompletter Quellcode:

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from telegram.ext import *


API_KEY = '123qwertzuiop1234567890qwertzui234567890'


def handle_message(update, context):
    # print(update, context)
    text = update.message.text

    response = create_responses(text)
    update.message.reply_text(response)


def create_responses(input_text):
    if input_text == 'hi':
        return 'Hey ho!'
    else:
        return 'Das habe ich nicht verstanden.'


def main():
    updater = Updater(API_KEY)
    dp = updater.dispatcher

    dp.add_handler(MessageHandler(Filters.text, handle_message))

    updater.start_polling(0)


if __name__ == "__main__":
    main()

```
```

</div>