---
id: 200
title: 'Python Telegram Bot &#8211; Dateien versenden'
date: '2021-12-12T11:05:10+00:00'
author: chris
layout: post
guid: 'https://christoph-schmalfuss.de/blog/?p=200'
permalink: /2021/12/12/python-telegram-bot-dateien-versenden/
image: 'http://christoph-schmalfuss.de/blog/wp-content/uploads/2021/12/Thumbnail-telsend-serioes.png'
categories:
    - API
    - 'Bots und Automatisierung'
---

<figure class="wp-block-image size-large">[![Das Bild zeigt ein Fenster mit der Aufschrift "Python Telegram". ](https://christoph-schmalfuss.de/blog/wp-content/uploads/2021/12/Thumbnail-telsend-serioes-1024x576.png)](https://www.youtube.com/watch?v=u-qQ01AmF9c)</figure>Lando hat gefragt, wie man mit einem Telegram Bot Dateien verschicken kann. Das ist eine schöne Frage und hier kommt die Antwort. Viel Freude!

Also, beim letzten Mal haben wir ja schon einen einfachen Bot erstellt, der Nachrichten senden und empfangen kann. Falls ihr das Tutorial noch nicht gesehen habt, dann findet ihr in der Videobeschreibung den Link zum entsprechenden Video.

Wir werden jetzt also den Code vom letzten Mal nehmen und so erweitern, dass unser Bot Dateien verschickt, wenn wir ihn darum bitten.

Als erstes brauchen wir einen weiteren Teil des Telegram-Pakets. Der nennt sich ‚Bot‘ und wir können den folgendermaßen importieren.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
from telegram.bot import Bot 
```
```

</div>## Unserem Bot das Senden beibringen

Als nächstes legen wir eine neue Funktion an. Die nennen wir send\_file. Und wenn wir die Funktion später nutzen, geben wir immer zwei Dinge mit. Natürlich eine Datei, also einfach die Datei, die wir senden wollen. Und außerdem werden wir der Funktion eine chat\_id mitgeben. Die wird dafür genutzt, dass unser Bot dann auch weiß, in welchen Chat er die Datei posten soll.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def send_file(file, chat_id):
    ...

```
```

</div>Die send\_file Funktion soll für uns jetzt drei Dinge machen. Sie soll erst ein Bot Objekt erzeugen, das für uns die Datei verschicken kann, dann eine Datei öffnen und dann die geöffnete Datei über unser Bot Objekt verschicken.

Fangen wir also mit dem Bot Objekt an. Das lässt sich ganz leicht mithilfe unseres API-Keys erstellen.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def send_file(file, chat_id):
    bot = Bot(token=API_KEY)
```
```

</div>Als nächstes wollen wir eine Datei öffnen, die wir danach versenden können.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def send_file(file, chat_id):
    bot = Bot(token=API_KEY)

    with open(file, 'r') as f:
```
```

</div>Und jetzt wollen wir die geladene Datei versenden. Das machen wir mit dem Befehl send\_document. Es gibt übrigens auch andere Funktionen wie send\_audio oder send\_video. Aber ich nutze am liebsten send\_document, weil da der Dateityp egal ist, den wir senden wollen. Bei send\_document müssen wir zwei Parameter mitgeben und zwar wieder unsere chat\_id und die Datei.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def send_file(file, chat_id):
    bot = Bot(token=API_KEY)

    with open(file, 'r') as f:
        bot.send_document(chat_id=chat_id, document=f)
```
```

</div>Jetzt ist es an der Zeit, eine kleine Testdatei zu erstellen. Wir erzeugen dafür jetzt einfach mal eine einfache Textdatei im Hauptordner unseres Projektes und nennen die Datei file.txt.

## Funktion aufrufen

Unsere Funktion zum Senden von Dateien ist jetzt schon funktionstüchtig, bleibt eigentlich nur noch die Fragen, wann wir die Funktion auslösen wollen. Wir können unseren Bot z.B. so programmieren, dass er uns die Datei schickt, sobald wir danach fragen. Also wenn ich dem Bot schreibe „Schick mir die Datei!“, dann soll er mir die Datei schicken.

Auch das ist eigentlich kein Problem. Dafür gehen wir jetzt wieder in die Funktion handle\_message, die wir beim letzten Mal erstellt haben. Zur Erinnerung: Das war die Funktion, die sich die eintrudelnden Nachrichten anschaut und entscheidet, was mit ihnen passieren soll.

Und in der Funktion müssen wir jetzt nur zwei Änderungen vornehmen. Einerseits brauchen wir für das senden einer Datei ja eine chat\_id und die lesen wir als erstes aus.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def handle_message(update, context):
    text = update.message.text
    chat_id = update.effective_chat.id              
    ...
```
```

</div>Und wir wollen ja, dass die chat\_id zum Erstellen der Antwort verwendet wird und deshalb schreiben wir die chat\_id mit in unsere create\_responses Funktion. Das war die Funktion, die die Antwortnachricht erstellt.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-python" data-lang="Python">```
def handle_message(update, context):
    text = update.message.text
    chat_id = update.effective_chat.id              
    response = create_responses(text, chat_id)      
    update.message.reply_text(response)
```
```

</div>Und die create\_responses Funktion soll die chat\_id dann natürlich auch annehmen, deshalb schreiben wir die chat\_id mit in die Liste der Sachen, die die Funktion create\_responses benutzen soll.

Die Funktion soll nun ja die Datei rausschicken, sobald wir ihr den Befehl dazu geben. Deshalb lassen wir die Funktion jetzt darauf warten, dass wir ihr schreiben „Schick die Datei!“.

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
    if input_text == "Schick die Datei!":          
        send_file('file.txt', chat_id)             

        return "Hier ist die Datei"                
```
```

</div>Und jetzt können wir das ganze auch schon ausprobieren. Und so einfach ist es also, mit Python über einen Telegram Bot Dateien zu verschicken.

## ✅ Kompletter Quellcode

<div class="hcb_wrap">```
<pre class="prism line-numbers lang-plain">```
from telegram.ext import *
from telegram.bot import Bot


API_KEY = '1234567890ß1234567890ß23456789'


def send_file(file, chat_id):
    bot = Bot(token=API_KEY)

    with open(file, 'r') as f:
        bot.send_document(chat_id=chat_id, document=f)


def handle_message(update, context):
    text = update.message.text
    chat_id = update.effective_chat.id
    response = create_responses(text, chat_id)
    update.message.reply_text(response)


def create_responses(input_text, chat_id):
    if input_text == "hi":
        return "Hey ho!"

    if input_text == "Schick die Datei!":
        send_file('file.txt', chat_id)

        return "Hier ist die Datei"   

    else:
        return "Das habe ich leider nicht verstanden."


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