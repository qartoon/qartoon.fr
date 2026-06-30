---
layout: post
title: Monsieur C
categories: [404 CTF 2026, OSINT]
tags: writeup
---

Here is my solution for the OSINT challenge **Monsieur C** as part of the 2026 edition of the [404CTF](https://404ctf.fr/) held online by the French secret service ([DGSE](https://www.dgse.gouv.fr/en)) and [Telecom SudParis](https://www.telecom-sudparis.eu/en/).

<br/>

----

<br/>

This problem is divided in **4** steps as followed :
- [Monsieur C Découverte](#monsieur-c--découverte) : **intro**
- [Monsieur C Somebody is watching me](#monsieur-c--somebody-is-watching-me) : **medium**
- [Monsieur C Voyage voyage](#monsieur-c--voyage-voyage) : **medium**
- [Monsieur C Fan de sciences](#monsieur-c--fan-de-sciences) : **hard**

## Monsieur C : Découverte

> Un étrange personnage se présentant comme "Monsieur C" est venu me voir, moi, créateur du chall, en DM pour faire de la pub pour son nouveau blog en partageant son URL. Il était si sympathique que je n'ai pu refuser et ai mis son URL dans le premier endroit que j'avais sous les yeux. Quel est l'URL du blog ?

We need to retrieve **Mister C's blog**. We know the author of the challenge (Sherpearce) advertised the **URL** somewhere.

I had a look at X, Instagram, Github and finally **Discord**. In the author's profile on the event's Discord server :

![Discord profile](/assets/img/404-ctf-2026/monsieur-c/discord-profile.jpg)

### 🚩 Flag
```
404CTF{lab.c.404ctf.fr}
```
## Monsieur C : Somebody is watching me

> L'individu surveillé cache probablement des informations d'importance capitale chez lui. D'après nos renseignements, il dispose d'un dispositif de surveillance à son domicile. Encore faut-il trouver un moyen d'y accéder...

From [lab.c.404ctf.fr/cv](https://lab.c.404ctf.fr/cv) hosting our target's resume, we get his name : **Carlos Int**

In a few blog posts, the target mentionned a **Youtube channel** that can be found easily using `"Carlos Int" site:youtube.com` : the channel is located at [youtube.com/@IntCarlos](https://www.youtube.com/@IntCarlos).

The channel hosts multiple videos and Shorts among which there is [Ma chambre](https://www.youtube.com/shorts/cR_RMPZ6QF8), a slideshow with fast-moving pictures of our target's room. One of them, holds a username and a password written on a whiteboard (`rootcam:W19ub7d08!`) :

![Short screenshot](/assets/img/404-ctf-2026/monsieur-c/short-screenshot.png)

I provided these credentials to the login page located at [lab.c.404ctf.fr/login](https://lab.c.404ctfr.fr/login) and was granted the access to `/camera` :

![Camera display](/assets/img/404-ctf-2026/monsieur-c/camera-display.png)

### ⁶🤷⁷ Flag

```
404CTF{67}
```

## Monsieur C : Voyage voyage

> Monsieur C est récemment parti en vacances. Il y a quelques siècles, un explorateur français s'était lui aussi rendu pour la première fois sur ce lieu, accompagné d'un naturaliste. Comment s'appelle ce naturaliste ?

Our target went on a trip lately. We need to find where and what French naturalist explored this location centuries ago.

On the Youtube channel, the video [Souvenirs](https://www.youtube.com/watch?v=Y-mu1x0LMZs) appears promising. While it **does not mention the destination explicitly**, we have hints **about** the location : **flowers** growing there, has both **beaches** and **mountains**, a **drawing** from someone he met there.

A reverse image search for the flowers leads to this page : [Leucheria leontopodioides - Pl@ntNet identify](https://identify.plantnet.org/the-plant-list/species/Leucheria%20leontopodioides%20\(Kuntze\)%20K.Schum./data).

![Flowers](/assets/img/404-ctf-2026/monsieur-c/flowers.png)

Leucheria is *native to South America and the Falkland Islands*[^1]. A quick search will then mention **Antoine-Joseph PERNETY** as the French naturalist who went on a expedition to the Falkland Islands with the explorer Louis-Antoine de Bougainville.
## 🚩 Flag
```
404CTF{antoine-joseph_pernety}
```
## Monsieur C : Fan de sciences

> Qui est le scientifique préféré de "Monsieur C" ?

From [lab.c.404ctf.fr/cv](https://lab.c.404ctf.fr/cv) hosting our target's resume, we get this phone number : **+33650237918**

On WhatsApp, the contact associated with this phone number is :

![WhatsApp profile](/assets/img/404-ctf-2026/monsieur-c/whatsapp-profile.jpg)

A reverse image search of the profile picture then leads to [Camille Guérin](https://fr.wikipedia.org/wiki/Camille_Gu%C3%A9rin)).
### 🚩 Flag
```
404CTF{camille_guerin}
```

[^1]: [Leucheria - Wikipedia](https://en.wikipedia.org/wiki/Leucheria)