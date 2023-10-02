---
title: Setting up the ComputeBlade Agent
layout: page
parent: Getting Started
permalink: "/getting-started/computeblade-agent/"
nav_order: 3
---

The [computeblade-agent](https://github.com/Uptime-Lab/computeblade-agent) is an OS agent interfacing with the ComputeBlade hardware.
It controls fan speed, LEDs and handles common events e.g. to identify/find an individual blade in a server rack.
In addition, it exposes hardware- and agent-related metrics on a Prometheus endpoint.

Detailed configuration options and install instructions are documented on the [GitHub Repo](https://github.com/uptime-lab/computeblade-agent). The **TL;DR** in case you just want to install it:
```bash
curl -L -o /tmp/computeblade-agent-installer.sh https://raw.githubusercontent.com/Uptime-Lab/computeblade-agent/main/hack/autoinstall.sh
chmod +x /tmp/computeblade-agent-installer.sh
/tmp/computeblade-agent-installer.sh
```

Here's a small demo video of the identify operation in-action:
[![Video](https://img.youtube.com/vi/ik-7X-YZQ9c/0.jpg)](https://youtu.be/ik-7X-YZQ9c)

