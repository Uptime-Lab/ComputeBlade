---
title: Flashing the bootloader
layout: page
parent: Compute Blade Dev
permalink: "/dev/bootloader/"
---
### Flashing the bootloader

To flash the bootloader, you need to turn on the Blade with the nRPIBOOT button pressed (a second after turning the Blade on, you can already release it).
You can turn it on from USB-C or PoE; it doesn't matter. To flash, you need to plug in a USB-C and switch the switch to USB-C (the switch can be switched during operation).

![bootloader-1](/assets/images/bootloader-1.png)

On a computer with Linux to which you will connect the Blade:

```bash
sudo apt install libusb-1.0-0-dev
git clone --depth=1 https://github.com/raspberrypi/usbboot
cd usbboot
make
cd recovery
nano boot.conf
```

change the line

```
BOOT_ORDER=0xf16
```

That means:

Try NVMe first, followed by SD then repeat.

You can find more about boot order by following this [link](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#BOOT_ORDER){:target="_blank"}.

Optionally, I also recommend correcting 0 to 1 on this line to enable UART on boot

```
BOOT_UART=1
```

![bootloader-2](/assets/images/bootloader-2.png)

To update to the latest bootloader version use [repo](https://github.com/raspberrypi/rpi-eeprom/tree/master/firmware){:target="_blank"} and the right link:

```bash
rm -f pieeprom.original.bin
curl -L -o pieeprom.original.bin  https://github.com/raspberrypi/rpi-eeprom/raw/master/firmware/stable/pieeprom-2022-12-07.bin
```

```bash
./update-pieeprom.sh
cd ../
sudo ./rpiboot -d recovery
```

If UART is connected, you will see the firmware status. If the HDMI port is connected, the screen will turn green.

on UART (you should use BOOT_UART=1 in boot.conf):

![bootloader-3](/assets/images/bootloader-3.png)

Check the bootloader version:

```bash
vcgencmd bootloader_version
```

Also, on the UART when booting:

![bootloader-4](/assets/images/bootloader-4.png)

If the screen is red and in the UART during flashing:

```
Bad signature pieeprom.bin
FATAL error-code 24
```

You are probably using the wrong pieeprom.original.bin image. The right one should be 512k in size.

pieeprom.original.bin

In my case, the problem was due to an incorrect link (**blob** in the path):

~~https://github.com/raspberrypi/rpi-eeprom/blob/master/firmware/stable/pieeprom-2022-09-02.bin~~The correct one:

https://github.com/raspberrypi/rpi-eeprom/raw/master/firmware/stable/pieeprom-2022-09-02.bin
