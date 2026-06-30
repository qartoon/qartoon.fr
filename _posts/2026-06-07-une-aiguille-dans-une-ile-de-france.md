---
layout: post
title: Une aiguille dans une Île-de-France
categories: [404 CTF 2026, OSINT]
tags: writeup
---

Here is my solution for the **hard** OSINT challenge **Une aiguille dans une Île-de-France** as part of the 2026 edition of the [404CTF](https://404ctf.fr/) held online by the French secret service ([DGSE](https://www.dgse.gouv.fr/en)) and [Telecom SudParis](https://www.telecom-sudparis.eu/en/).

<br/>

----

<br/>

We are told that 2 threat actors are planning an attack towards **a scientist** to steal an award from her. They were traced and we are given the text message below, as well as a list of **1000 points of interest** under `points_d_interets.json` :

![Text message](/assets/img/404-ctf-2026/une-aiguille-dans-une-ile-de-france/text-message.jpg)

> I'll be waiting for you by the small rectangular fountain on the sidewalk facing the café. Don't forget your lock-picking kit !

We need to provide the name of the **great female scientist** living there.

## Finding the location among all POIs

I started using [Overpass turbo](https://overpass-turbo.eu/) to shorten the list of POIs. Given the details provided by the text message, I wrote this query :
```sql
(
    node(around:500,48.683432,2.296373)["amenity"="fountain"];
    [...]
    node(around:500,48.895186,2.440037)["amenity"="fountain"];
)->.fountains;

node(around.fountains:100)["amenity"~"cafe|bar|restaurant"]["name"~"cafe|café", i];

out;
```

It looks for all **fountains located in a 500-meter range** around each POI. Given this list, all **cafés located at 100 meters at most** from a fountain are returned. This last filter is based on the word "café" in the name (case insensitive).

As a result, I got **22 nodes**. I assumed "great female scientist" was too vague to be in Paris, so I focused on the **6 remaining nodes**.

![Overpass turbo results](/assets/img/404-ctf-2026/une-aiguille-dans-une-ile-de-france/results.png)

I then had a look at each of them using **Google Street View**. The location that best matched the description from the text message is [Labriz' Cafe](https://www.openstreetmap.org/node/6945843341), in Viroflay.

![Best location](/assets/img/404-ctf-2026/une-aiguille-dans-une-ile-de-france/best-location.png)

## The great scientist

I struggled a while to find a female scientist living in **Viroflay** ...

... only to find out this basic Google Search was suficient 🥲
![Google search](/assets/img/404-ctf-2026/une-aiguille-dans-une-ile-de-france/search.png)

On page 11 of this journal, I found the following article :
![Article](/assets/img/404-ctf-2026/une-aiguille-dans-une-ile-de-france/article.png)

## 🚩 Flag

```
404CTF{catherine-cesarsky}
```