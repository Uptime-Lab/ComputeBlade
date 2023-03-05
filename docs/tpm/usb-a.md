---
title: USB-A
layout: page
parent: Compute Blade TPM and Dev
permalink: "/tpm-and-dev/usb-a/"
---

## USB-A

To turn on the USB-A port to access the operating system on the Blade, add the following line to the config.txt:

```bash
dtoverlay=dwc2,dr_mode=host
```

