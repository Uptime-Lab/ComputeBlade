---
title: Flashing OS to eMMC / accessing eMMC
layout: page
parent: Compute Blade Dev
permalink: "/dev/flashing-os/"
---
### Flashing OS to eMMC / accessing eMMC

In short, it's like this:

- On a computer with Linux to which you will connect the Blade


```bash
sudo apt install libusb-1.0-0-dev
git clone --depth=1 https://github.com/raspberrypi/usbboot
cd usbboot
make
cd recovery
sudo ./rpiboot
```

If you have a Mac OS you need [Homebrew](https://brew.sh/){:target="_blank"}

```bash
brew install pkgconfig libusb
```
- Slide the USB switch to USB-C. Press Boot (nRPIBOOT) on the Blade and connect it to your Linux/Mac with USB-C cable


- After that you will be able to mount the Boot partition if present. (it usually happens automatically). Note a stock CM4 has a completely empty eMMC.

You can fix your files/configs or install the OS using the [Raspberry Pi Imager](https://www.raspberrypi.com/software/){:target="_blank"}

For complete instructions, see Jeff Geerling's website: [instructions](https://www.jeffgeerling.com/blog/2020/how-flash-raspberry-pi-os-compute-module-4-emmc-usbboot){:target="_blank"} 
