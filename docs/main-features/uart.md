---
title: UART
layout: page
parent: Main Features (Basic Blade)
permalink: "/main-features/uart/"
nav_order: 2
---
This is the same UART0 port, but with the big one, you can use 5V in/out (in "in" mode ONLY if the Blade has no other power source)

{: .note }
> Connect "correctly":
> * RX -> TX
> * TX -> RX
> * GND -> GND

in config:
```bash
enable_uart=1
```

You can [change the bootloader setting](/dev/bootloader/) to enable UART from the boot.
Add this line to boot.conf and flash the bootloader:
```bash
BOOT_UART=1
```
Follow [this link](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#BOOT_UART){:target="_blank"} to the Raspberry Pi Documentation BOOT_UART value

![uart-1](/assets/images/uart-1.png)
![uart-2](/assets/images/uart-2.png)