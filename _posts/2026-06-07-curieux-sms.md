---
layout: post
title: Curieux SMS
categories: [404 CTF 2026, Forensics]
tags: writeup
---

Here is my solution for the **easy** forensic challenge **Curieux SMS** as part of the 2026 edition of the [404CTF](https://404ctf.fr/) held online by the French secret service ([DGSE](https://www.dgse.gouv.fr/en)) and [Telecom SudParis](https://www.telecom-sudparis.eu/en/).

<br/>

----

<br/>

We are given `chall.zip` holding the following files :
```
├───1
    └───mmssms.db
├───2
    └───mmssms.db
└───3
    └───app_parts
        └───1
        [...]
        └───131
    └───mmssms.db
```

A quick search for the keyword `mmssms.db` indicates they are databases residing on most **Android** devices. These files hold highly valuable data for forensic investigations such as : **conversation history, text message content, attachments**. Additional details in [this Magnet Forensics' blogpost](https://www.magnetforensics.com/blog/android-messaging-forensics-sms-mms-and-beyond/).

Let's have a look into these using **DB Browser for SQLite**.

## /1/mmssms.db

This database holds **3 tables** : `pdu`, `sms_restricted` and `sms`. In this last table, in the body of message ID 6, I found what appears to be the first part of the flag :
```
Le mot de passe pour accéder au dossier est  404CTF{m4r13_
```

## /2/mmssms.db

This one holds **7 tables** including `conversation` with one single row. The `snippet_text` field must be the second part of the flag, **Marie Curie** being a famous French physicist and chemist :
```
cur13_
```

## /3/mmssms.db

This final database file contains the table `pdu` (stands for Protocol Data Unit). From my understanding, this is data **related to MMS** and **associated attachments**.
However, **in the single row** we have what appears to be the last part of the flag in `sub`:
```
1898}
```
Since **1898** is the year **radium** and **polonium** were discovered by **Marie Curie** and her husband, I assumed this was sufficient and submitted `404CTF{m4r13_cur13_1898}`. It failed... 😭

Then, I remembered I had no use of the `app_parts` folder for now.

## /3/app_parts/

The `app_parts` folder holds **92 raw files** numbered **from 1 to 131**. Running the `file` command against these files will produce :
```
$ file ./3/app_parts/*

./1:   data
[...]
./62:  JPEG image data, JFIF standard 1.01, resolution (DPI), density 96x96, segment length 16, baseline, precision 8, 195x109, components 3
```

This is it ! We have our missing part :
![62 content](/assets/img/404-ctf-2026/curieux-sms/62-content.png)

## 🚩 Flag
```
404CTF{m4r13_cur13_r4d1um_1898}
```