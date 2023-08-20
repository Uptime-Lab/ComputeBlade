---
title: RasberryPi compared to regular x86/64 processors
layout: page
parent: Getting Started
permalink: "/getting-started/rpi-compare-x86/"
nav_order: 2
---

This page compares the RaspberryPi platform against regular commodity hardware (x86/64) and things to watch out for.


# x86/amd64 vs ARM64 architecture

The x86 platform, prevalent in regular computers, offers robust performance, broad software compatibility, and a variety of operating system options. It's well-suited for resource-intensive tasks, software development, and versatile computing needs.

In contrast, the ARM64 platform, exemplified by the RaspberryPi, prioritizes power efficiency, compact form factors, and IoT/embedded applications. With a strong Linux ecosystem, ARM64 devices are tailored for specialized projects, educational exploration, and scenarios where low power consumption and small size are paramount.

Ultimately, the choice between x86 and ARM64 depends on the intended purpose, ranging from high-performance computing to energy-efficient projects and hands-on learning experiences.

The software support for ARM64 is gaining significant improvements since 2022, when Apple switched its notebooks to the same architecture.

While not being as powerful compared to a regular Server, the RaspberryPi Compute Module can run demanding software while keeping power consumption low.
This allows high-density dedicated servers (aka the ComputeBlade) running without having a full datacenter in the basement.



# Compatibility
Given the difference in architecture, the RaspberryPi does not support all software out of the box.
However, no ARM64 support is the exception rather than the rule.


# Boot Process Differences: x86 vs. ARM64 (RaspberryPi)

The boot process of x86 and ARM64 platforms, such as the RaspberryPi, diverges due to architectural distinctions and hardware considerations:

### x86 Boot Process:
1. **Firmware:* x86 computers typically use BIOS (Basic Input/Output System) or UEFI (Unified Extensible Firmware Interface) as their firmware. These firmware interfaces initialize hardware components, locate the boot device, and load the bootloader.

2. **Bootloader:** The bootloader, often GRUB or similar software, loads the operating system kernel from the boot device (usually a hard drive or SSD). It also handles the selection of the desired operating system if multiple options are available.

3. **Kernel Initiation:** Once the bootloader hands off control to the operating system kernel, the kernel initializes the hardware, mounts the root filesystem, and starts the user-space processes.

### ARM64 Boot Process (RaspberryPi):
> More details can be found in the [official documentation](https://www.raspberrypi.com/documentation/computers/compute-module.html).

1. **Firmware:** The RaspberryPi uses a specialized bootloader known as the RaspberryPi Bootloader (often referred to as `bootcode.bin`). This firmware, stored in the boot partition of the SD card, initializes the ARM processor cores, memory, and peripherals.

2. **GPU Firmware:** The GPU firmware (included in `bootcode.bin`) initializes the VideoCore GPU and loads the initial kernel image (`kernel.img`) into memory.

3. **ARM64 Kernel:** The loaded kernel initializes the ARM64 processor cores, configures memory, and starts essential kernel processes. The kernel is typically paired with a device tree blob (`*.dtb` file) that describes the hardware configuration.

4. **Kernel Initiation:** Once the ARM64 kernel is operational, it mounts the root filesystem, initializes drivers, and launches user-space processes.

The ARM64 boot process for the RaspberryPi involves a multi-stage process that leverages the GPU firmware and a specialized bootloader, ultimately loading the ARM64 kernel and initializing the system. In contrast, x86 systems use more standardized firmware interfaces and bootloaders, similar to those found in traditional desktop and laptop computers.

These differences reflect the distinct hardware architectures of x86 and ARM64 platforms, influencing how the system initializes and loads the operating system.


## U-Boot, UEFI and more

Once working with more specific operating systems for the RaspberryPi, projects like [u-boot](http://u-boot.readthedocs.io) or [pftf/RPI4](https://github.com/pftf/RPi4) (UEFI for RaspberryPi 4) appear.

Without going into too much detail here, both are more standardised bootloaders with u-boot being very specific for embedded devices and UEFI being a more mainstream solution.
In the context of the RaspberryPi, both are loaded **instead** of the Linux kernel directly.

Once executed, they take care of further initialising the hardware and loading the actual Linux kernel.
E.g. [Talos Linux](http://talos.dev), a tailored distribution of Kubernetes, uses u-boot for all of its supported embedded boards where it acts as a standardisation layer of the boot process.
