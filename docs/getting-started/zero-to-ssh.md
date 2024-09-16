---
title: From Zero to SSH
layout: page
parent: Getting Started
permalink: "/getting-started/zero-to-ssh/"
nav_order: 1
---

This getting started guide is intended to provide a generic starting ground, covering all steps required to get an SSH session to your blade.
While you can use the Blade with an SD-Card or the embedded eMMC as boot drive, this guide focuses on using the NVMe drive.

# 0. Checklist

- [ ] A PoE capable switch (802.3af or 802.3at). [Here](/main-features/ethernet/) is a list of known-working models.
- [ ] A LAN cable
- [ ] Any version of the ComputeBlade (check [here](/) for details )
- [ ] A [Raspberry Pi Compute Module 4 (CM4)](https://www.raspberrypi.com/products/compute-module-4/?variant=raspberry-pi-cm4001000). In case you plan running [Kubernetes](http://kubernetes.io) on it, make sure to get at least 4GB of memory.
- [ ] An NVMe SSD. Any capacity works, ~500GB seems to be the sweet-spot as of July 2023. A list of already verified drives is located [here](/supported-ssds/).
- [ ] (recommended) A heatsink for the CM4
- [ ] An NVMe to USB adapter. The cheapest option supporting PCIe-based NVMe drives should work.

# 1. Setting up the hardware

1. Install the CM4 on the ComputeBlade
Make sure to line up the CM4 in the correct orientation. It fits only one way! Apply gentle downward facing pressure to the CM4 - you will hear the connectors snapping in.


2. Install the heatsink on the CM4.
Make sure there is sufficient height clearance, when not using the heatsink offered by the ComputeBlade project

3. Plug everything into your PoE switch
This is just a sanity check to see if everything was installed properly!
The LEDs should power on. If they do not, something is not installed correctly or your switch might be incompatible.

4. Unplug the ComputeBlade again
As stated in (3), this was just a sanity check.

# 2. Setting up the OperatingSystem on the NVMe SSD

{: .note }
Depending on when you bought your CM4, you might have to upgrade the firmware first. Check [here]() for more details!

## 2.1. Choose an Operating System
> Make sure to choose the 64bit versions!

There are several supported OSes supported by the RaspberryPi, **but** not all are able to boot from the NVMe SSD out of the box.
We recommend you to choose one of the followings:
- [Ubuntu 22.04 LTS](https://ubuntu.com/download/raspberry-pi/thank-you?version=24.04&architecture=server-arm64+raspi) (NVME support starting with 22.04.2)
- [Ubuntu 23.04](https://ubuntu.com/download/raspberry-pi/thank-you?version=23.04&architecture=server-arm64+raspi) (NVME support starting with 22.04.2) (The Linux Kernel 6.2 shows some performance improvements for some NVMe drives)
- [Raspberry Pi OS Lite](https://www.raspberrypi.com/software/)

## 2.2. Flash the Operating System on the NVMe drive

### 2.2.1 Install the NVMe drive in the USB-to-NVMe adapter

Make sure the drive is placed in the connector and does not disconnect when you plug it into your computer.
In case your adapter comes with an enclosure, you don't have to install it, as you'll remove the drive very soon again.


### 2.2.2 Use the official RaspberryPi Imager to flash your OS
> As stated in 2.1., make sure to choose the 64 bit version.

1. Install the latest version of the [Raspberry Pi Imager](https://www.raspberrypi.com/software/)
2. Choose your desired OS. The 64bit lite version of Raspberry Pi OS is located in the *Raspberry Pi OS (other)* section. Ubuntu can be found in *Other general-purpose OS*.
3. Click the settings icon on the bottom right and configure the hostname (e.g. `blade0`), Enabel SSH and set username and password. As a security best-practice, it's recommended to enforce public-key authentication. In case this is new for you, use the password authentication - you'll get to it while playing around with Linux!
4. Choose the storage. Your NVMe drive should show up here! If it does not, something went wrong. Check if it is plugged in your computer and the NVMe drive is installed correctly on it.


# 3. Finalizing your Blade
1. Remove the NvMe drive from the adapter
2. Install it on the Blade
3. Connect the Blade to your PoE switch
4. Wait a few minutes for it to boot. Give it some time! The first boot expands the root file system to accomodate your SSD capacity
5. Connect to your blade via SSH. You can check the DHCP leases in your router for the hostname configured in (2.2.2) or rely on mDNS (works for Ubuntu 23.04 only): `ssh <username>@<hostname>.local`, e.g. `ssh xvzf@blade0.local`
6. *COMING SOON*: Install the ComputeBlade Agent to auto-configure LEDs and the [FAN-Unit](/main-features/fan-unit-connector/)


# 4. Next Steps

**Do whatever you want!**

Here are some inspirations:
- Build a Kubernetes homelab for testing
- Power your smarthome using [HomeAssistant](https://www.home-assistant.io) on your blade.
- Run your own CICD workloads on it, e.g. by hosting your own [Github Actions Runner](https://docs.github.com/en/actions/hosting-your-own-runners)
- Run your own backup-server Blade with Timemachine (e.g. using [this](https://hub.docker.com/r/mbentley/timemachine) docker image)
- Host a custom Discord-Bot, just like the [one powering the UptimeLab Discord](https://github.com/Uptime-Lab/Uptime-Bot).

