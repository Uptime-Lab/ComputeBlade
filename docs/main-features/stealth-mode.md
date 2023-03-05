---
title: Stealth mode
layout: page
parent: Main Features (Basic Blade)
permalink: "/main-features/stealth-mode/"
---

## Stealth mode

Stealth mode will turn off all but the Digital LEDs at once. It is implemented via a GPIO and a transistor, which means it won't harm the Blade functionality. It is possible to change the brightness using software PWM however in some cases, it may not work perfectly.



Compute Blade RC2 cannot turn off the LEDs on the Ethernet port this way, but they can be turned off in other ways. The Digital LEDs will also not be turned off due to technical limitations, but since they are controlled from the GPIO this should not be a problem.\



Initialization in the terminal:

```bash
echo "21" > /sys/class/gpio/export
echo "out" > /sys/class/gpio/gpio21/direction
```

To turn off the LEDs:


```bash
echo "1" > /sys/class/gpio/gpio21/value
```

To turn on the LEDs:


```bash
echo "0" > /sys/class/gpio/gpio21/value
```

To do this immediately after booting the OS, you can add these commands to /etc/rc.local:


```bash
sudo nano /etc/rc.local
```

```bash
#!/bin/sh -e
#
# rc.local
#

echo "21" > /sys/class/gpio/export
sleep 0.1
echo "out" > /sys/class/gpio/gpio21/direction
echo "1" > /sys/class/gpio/gpio21/value
sleep 0.1

exit 0
```

