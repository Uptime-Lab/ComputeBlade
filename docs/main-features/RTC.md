---
title: Real-Time Clocks
layout: page
parent: Compute blade headers
grand_parent: Main Features (Basic Blade)
permalink: "/main-features/headers/rtc/"
nav_order: 1
---
### Using and configuring the RTC module
![rtc](/assets/images/rtc.jpg)

In config:
```bash
dtoverlay=i2c-rtc,ds3231
dtparam=i2c_arm=on
```

Reboot and then check it in the terminal that the i2c device is available:

```bash
sudo i2cdetect -l|sort
sudo i2cdetect -y 1 
```

Next is the setup:

```bash
sudo apt-get -y remove fake-hwclock
sudo update-rc.d -f fake-hwclock remove
sudo systemctl disable fake-hwclock
```

Edit the file **hwclock-set**:

```bash
sudo nano /lib/udev/hwclock-set
```
Complete file:
```bash
#!/bin/sh
# Reset the System Clock to UTC if the hardware clock from which it
# was copied by the kernel was in localtime.

dev=$1

#if [ -e /run/systemd/system ] ; then
#    exit 0
#fi

if [ -e /run/udev/hwclock-set ]; then
    exit 0
fi

if [ -f /etc/default/rcS ] ; then
    . /etc/default/rcS
fi

# These defaults are user-overridable in /etc/default/hwclock
BADYEAR=no
HWCLOCKACCESS=yes
HWCLOCKPARS=
HCTOSYS_DEVICE=rtc0
if [ -f /etc/default/hwclock ] ; then
    . /etc/default/hwclock
fi

if [ yes = "$BADYEAR" ] ; then
#    /sbin/hwclock --rtc=$dev --systz --badyear
    /sbin/hwclock --rtc=$dev --hctosys --badyear
else
#    /sbin/hwclock --rtc=$dev --systz
    /sbin/hwclock --rtc=$dev --hctosys
fi

# Note 'touch' may not be available in initramfs
> /run/udev/hwclock-set
```

Reboot and check in terminal:

```bash
timedatectl status
```

Read:

```bash
sudo hwclock -r
```

Write:

```bash
sudo hwclock -w
```

Additional info

```bash
sudo hwclock --verbose
```

