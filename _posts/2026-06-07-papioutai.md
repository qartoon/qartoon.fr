---
layout: post
title: Papioutai
categories: [404 CTF 2026, OSINT]
tags: writeup
---

Here is my solution for the **easy** OSINT challenge **Papioutai** as part of the 2026 edition of the [404CTF](https://404ctf.fr/) held online by the French secret service ([DGSE](https://www.dgse.gouv.fr/en)) and [Telecom SudParis](https://www.telecom-sudparis.eu/en/).

<br/>

----

<br/>

We will act as genealogists in this case and we are tasked to provide the following details about someone named **Jean Roux** :
- his **graduation year** at the ENS (Ecole Normale Supérieure)
- his **birth town**

We know he died during World War I in a place ending with "demanges".

> Ahlala, l'ENS, cette école qui a produit tant d'esprits savants ! Une amie aimerait que vous l'aididez à retrouver des informations sur son bisaïeul, Jean Roux, ancien Ulmien mort pour la France en 14-18 dans un lieu dont le nom finit par demanges. Saurez-vous retrouver l'année de promotion de Jean Roux, ainsi que sa ville de naissance ? Format : 404CTF{1876_saint-germain-en-hyères}

## Graduation year

A yearbook is available at [archicubes.ens.fr/lannuaire](https://archicubes.ens.fr/lannuaire) :

![Yearbook search](/assets/img/404-ctf-2026/papioutai/yearbook-search.png)

**Jean Roux** was graduated in **1912**.

## Birth town

Since our target died at war between **1914** and **1918**, I used the search engine located at [memoiredeshommes.gouv.fr](https://www.memoiredeshommes.defense.gouv.fr/conflits-et-operations-2/premiere-guerre-mondiale/morts-pour-la-france-de-la-premiere-guerre-mondiale/faire-une-recherche). I got around **30 search results** but only [one of them](https://www.memoiredeshommes.defense.gouv.fr:443/ark:40699/m005239ff9660d6c.moteur=arko_default_670f920646a08) died in **Courdemanges** :

![Birth and death dates](/assets/img/404-ctf-2026/papioutai/birth-death-dates.png)

He was born in **Saint-Estèphe** in 1893.

## 🚩 Flag
```
404CTF{1912_saint-estephe}
```


