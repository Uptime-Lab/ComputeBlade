---
title: PoE+ indication
layout: page
parent: Main Features (Basic Blade)
permalink: "/main-features/poe-indication/"
nav_order: 4
---

You can use it to monitor power supply failures or limit yourself in overclocking
LED with "+" and GPIO23 indicate the operating mode:

* Green - 5-volt present: PoE or USB-C or 5v direct
* GPIO23 Low

![uart-1](/assets/images/poe-low.png)

* Orange (Green and Red together) - 802.3at Type 2 operating mode, PoE+
* GPIO23 High
* Blade can take up to 30W power (22W for RC2)

![uart-1](/assets/images/poe-high.png)