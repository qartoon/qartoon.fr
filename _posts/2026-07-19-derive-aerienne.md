---
layout: post
title: Dérive aérienne
date: 2026-07-19 00:00:00
categories: [Shutlock CTF 2026, Networking]
tags: [writeup, shutlock, networking]
---

Here is my solution for the **easy** networking challenge **Dérive aérienne** as part of the 2026 edition of the [Shutlock CTF](https://shutlock.fr/) held online by the French special intelligence service ([DGSI](https://dgsi.interieur.gouv.fr/english/)) and [EPITA](https://www.epita.fr/en/).

<br/>

----

<br/>

A drone entered a restricted area without prior authorization. Hopefully, a network flow was captured during the flight and is provided under `drone.pcap`.

## Overview

All packets are UDP from and towards port **14550**. Speedguide[^1] references this port as being used for MAVLink ground station protocol whose documentation is available at [mavlink.io](https://mavlink.io/en/guide/serialization.html#v1_packet_format).

![Wireshark capture](/assets/img/shutlock-ctf-2026/derive-aerienne/wireshark-capture.png)

## Decoding packets

I was able to find a LUA plugin on Github at [dagar/mavlink_common.lua](https://gist.github.com/dagar/c006ce6014fd56fbdab92af062bd8e19). After copying the file to the appropriate folder and reloading the plugins (*Analyse > Reload Lua Plugins*), I noticed 2 distinct packet types :
- `HEARTBEAT`
- `GLOBAL_POSITION_INT`

This last packet type hold valuable data to describe the position of the drone :
![Data fields](/assets/img/shutlock-ctf-2026/derive-aerienne/global-position-int.png) 

## Visualize the flight

Based on the latitudes and longitudes provided, I wrote a basic Python script that runs over a CSV data export from Wireshark using Pyplot from the Matplotlib package :
```python
import pandas as pd
import matplotlib.pyplot as plt

with open("lat_lon.csv", "r") as fi:
    df = pd.read_csv(fi)

plt.plot(df.get("lon (int32)"), df.get("lat (int32)"))
plt.show()
```

This produced the following graph representing the flag :
![Graph](/assets/img/shutlock-ctf-2026/derive-aerienne/graph.png)

## 🚩 Flag

```
SHLK{L3_C13L_35T_4_N0U5}
```

[^1]: [Port 14550 (tcp/udp) :: SpeedGuide](https://www.speedguide.net/port.php?port=14550)