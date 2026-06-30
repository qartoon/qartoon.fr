---
layout: post
title: Extraction d'ADNS
categories: [404 CTF 2026, Forensics]
tags: writeup
---

Here is my solution for the **easy** forensic challenge **Extraction d'ADNs** as part of the 2026 edition of the [404CTF](https://404ctf.fr/) held online by the French secret service ([DGSE](https://www.dgse.gouv.fr/en)) and [Telecom SudParis](https://www.telecom-sudparis.eu/en/).

<br/>

----

<br/>

We are given a **pcap** file along with the following text stating that the confidential results of an experiment have leaked, and we are tasked to uncover how.
> Les résultats confidentiels d'une expérience ont fuité. À vous de découvrir comment. /!\ Attention à ne visiter aucun lien contenu dans cette capture réseau /!\

## Technique identification

Opening the file with **Wireshark** quickly reveals a **DNS exfiltration** pattern which is consistent with the name of the challenge.

I filtered on `udp.dstport == 53` to keep queries only, and `dns.qry.type == 1` to remove duplicates since queries are sent for both record types **A** (`1`) and **AAAA** (`28`) :

![Wireshark screenshot](/assets/img/404-ctf-2026/extraction-d-adns/wireshark-screenshot.png)

## Reassembling

Once I got the relevant data out of this packet capture, I exported this analysis to `dns.csv` and printed out the concatenation of subdomains using **python** and **pandas** :

```python
import pandas as pd
import re

df = pd.read_csv("dns.csv")

for d in df.Name:
  r = re.findall(r"www\.(\w+?)\.(\w+?)\.(?:com|fr)$", d)
  print(end=r[0][0])
```

I got the following **base-32-encoded** string :
```
kjeumrrwaeaaav2fijifmubyjquqcaaaf4vucdaab4yp74z777zr66ea4nwjxy2efotw5zyaw3qsi2cpmjyyfhhtxcr6ibtqapojcz6h4eac5mz56qhd6fn7uvp5uent76iexcui7yzxbw2isglxsd26mf7sncf7yw2eyk4tp5xjdjxqoqi323wwz5skdnfqrwf4azriryz6cm2y2flg2zoqfc5kn6it5kgq27iu4eag27acs2hnkm6brhjvdhlt46ogunf7mp3fm4iakktpmr4paqd44qancit2co42envhanss6yvquy6oovx6tnmp3vtonkmrdly6zsol5jvqpbjbjdqwi2utlopi3voyqgcjibzle4d4n236o5bya4zlvkvmvjye3ykkqzg6yyp6dgkrqzx2id4anvsfmjeoxsgqyxqrtr4f7u3jmxrexqn6uy7jgwcmx4tbgz6ckpyp6dddx4j2j7ljtjnx54keoutur6e5p3vi77j7i4aaa
```

## Formatting

Handing this out to **CyberChef** :

![CyberChef base-32 decode](/assets/img/404-ctf-2026/extraction-d-adns/cyberchef-screenshot-1.png)

The magic wand appears : **CyberChef** noticed the magic number for the **webp** file format !

Once the suggested *Render image* filter is applied, we get this output :

![CyberChef rendered image](/assets/img/404-ctf-2026/extraction-d-adns/cyberchef-screenshot-2.png)

## 🚩 Flag

```
404CTF{CL4UD3_B3RN4RD_G0T_PWNED}
```