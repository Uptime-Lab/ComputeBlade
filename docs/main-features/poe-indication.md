---
title: PoE+ indication
layout: page
parent: Main Features (Basic Blade)
permalink: "/main-features/poe-indication/"
nav_order: 4
---

# PoE+ Indicator


The PoE+ Indicator can be used to monitor power supply failures or automate RaspberryPi overclocking, when power is provided via 802.3af only.
There is an LED on the Blade with a `+` label indicating the PoE+ power state.
Alongside, GPIO23 can be used to identify the power state.

|--------------------|--------------------------------------------|----------|----------------|
| LED Color          | Description                                | GPIO 23  | Power          |
|--------------------|--------------------------------------------|----------|----------------|
| Red                | 5 Volt present (PoE or USB-C or 5v direct) | **HIGH** | 12W            |
| Orange (Red+Green) | PoE+ (802.3at) present                     | **LOW**  | 25W (RC2: 22W) |
|--------------------|--------------------------------------------|----------|----------------|

<table>
  <tr>
    <td>
        <img src="/assets/images/poe-high.png"  alt="1">
        <h3>PoE or USB-C or 5v direct </h3>
    </td>
    <td>
        <img src="/assets/images/poe-low.png"  alt="1">
        <h3>PoE+ Detected </h3>
    </td>
   </tr>
</table>


## Accessing the PoE+ status in software

The GPIO23 indicates the PoE+ state, this Python script can e.g. used to detect the status.

```python
import RPi.GPIO as GPIO
import time

POE_INDICATOR_GPIO = 23

GPIO.setmode(GPIO.BCM)
GPIO.setup(POE_INDICATOR_GPIO, GPIO.IN, pull_up_down=GPIO.PUD_UP) # PoE indicator

try:
     button_state = GPIO.input(POE_INDICATOR_GPIO)
     if button_state == False:
        print("Powersource: 802.3at")
    else:
        print("Powersource: 802.3af or USB-C")
except:
    GPIO.cleanup()
```
