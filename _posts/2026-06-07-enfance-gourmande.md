---
layout: post
title: Enfance gourmande
categories: writeups
tags: 404ctf osint
---

Here is my solution for the **medium** OSINT challenge **Enfance gourmande** as part of the 2026 edition of the [404CTF](https://404ctf.fr/) held online by the French secret service ([DGSE](https://www.dgse.gouv.fr/en)) and [Telecom SudParis](https://www.telecom-sudparis.eu/en/).

<br/>

----

<br/>

We are given a **video representing one's memories** of a restaurant and an **item from the menu** ("*l'entrecôte de boeuf cuite au barbecue, accompagnée des légumes du potager du Roi*"). The visit occurred **before New Year's Eve, during Covid-19 lockdown**, in France. The flag is composed with the **name of the hotel** and the **price of the meal**.

Here are screenshots from the video :

![Memories 1](/assets/writeups/enfance-gourmande/memories-1.png)
![Memories 2](/assets/writeups/enfance-gourmande/memories-2.png)
![Memories 3](/assets/writeups/enfance-gourmande/memories-3.png)

## Approximate location

Using the third screenshot above, I knew the restaurant was located somewhere around **Versailles** using notable locations such as the **basilica of the Sacred Heart** (yellow), the **Eiffel tower** (red) and the **Montparnasse tower** (blue).

![Map](/assets/writeups/enfance-gourmande/notable-locations.png)
![Map](/assets/writeups/enfance-gourmande/map.png)
## Identifying the restaurant

**Screenshot 1** shows that the restaurant is part of [Relais & Châteaux](https://www.relaischateaux.com/gb/about/commitments-relaischateaux/). A member list and a map are available [here](https://www.relaischateaux.com/gb/themes/gastronomy-restaurants/). These 2 restaurants meet the requirements :
- [Le Corot](https://www.relaischateaux.com/gb/restaurant/le-corot/), located in **Avray**
- [La Table des Lumières](https://www.relaischateaux.com/gb/restaurant/les-lumieres-versailles/), located in **Versailles**

However, only *Le Corot* is located **near a lake** as suggested by **screenshot 2**. The name of the associated hotel is *Les Étangs de Corot* : [etangs-corot.com](https://www.etangs-corot.com/fr/).
## Retrieving the price of the meal

France was affected by 3 lockdowns during the Covid-19 pandemic[^1] :
 - From **March 17** to **May 11, 2020**
 - From **October 30** to **December 15, 2020**
 - From **April 3** to **May 3, 2021**

Our target must have visited the restaurant **in late 2020**.

Using [Wayback Machine](https://web.archive.org/), I found an archive of [etangs-corot.com](https://www.etangs-corot.com/fr/) from **November 30, 2020** and the menu at : [etangs-de-corot.myshopify.com/collections/notre-carte-a-emporter](https://web.archive.org/web/20201130230946/https://etangs-de-corot.myshopify.com/collections/notre-carte-a-emporter)

![Menu](/assets/writeups/enfance-gourmande/menu.png)

Back then, the meal was worth **60€**.
## 🚩 Flag
```
404CTF{les_etangs_de_corot-60}
```

[^1]: [Confinements liés à la pandémie de Covid-19 en France - Wikipédia](https://fr.wikipedia.org/wiki/Confinements_li%C3%A9s_%C3%A0_la_pand%C3%A9mie_de_Covid-19_en_France)