---
title: TPM and Secure Boot
layout: page
parent: Compute Blade TPM and Dev
permalink: "/tpm-and-dev/tpm/"
---
## TPM

In config:

```bash
dtparam=spi=on dtoverlay=tpm-slb9670
```

To check

In terminal:

```bash
mkdir infineon-tpm 
git clone https://github.com/infineon/eltt2
cd eltt2
make
sudo ./eltt2 -g
cd ..
```

For more information, please see these links:
[https://www.infineon.com/dgdl/Infineon-OPTIGA-TPM-Quick-Start-Guide-AdditionalProductInformation-v03_00-EN.pdf](https://www.infineon.com/dgdl/Infineon-OPTIGA-TPM-Quick-Start-Guide-AdditionalProductInformation-v03_00-EN.pdf){:target="_blank"}

[https://aws.amazon.com/ru/blogs/iot/using-a-trusted-platform-module-for-endpoint-device-security-in-aws-iot-greengrass/](https://aws.amazon.com/ru/blogs/iot/using-a-trusted-platform-module-for-endpoint-device-security-in-aws-iot-greengrass/){:target="_blank"}

## Secure Boot

At the end of 2022, Secure Boot support appeared.

Secure boot is a mechanism for verifying the integrity of the kernel+initramfs and other files required during boot by storing them in a signed ramdisk image. These files include the GPU firmware (start.elf etc), kernel, initrd, Device Tree and overlays.

Secure Boot Quickstart:

[https://github.com/raspberrypi/...](https://github.com/raspberrypi/usbboot/blob/master/secure-boot-example/README.md){:target="_blank"}