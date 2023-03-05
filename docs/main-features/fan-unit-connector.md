---
title: Square connector
layout: page
parent: Main Features (Basic Blade)
permalink: "/main-features/fan-unit-connector/"
---
## Square connector at the rear of the Blade

The square connector at the end of the Blade main purpose is to connect a Fan Unit.
The output is 5V and should work with any fan that supports 5V. The speed of the fan can be controlled with PWM.

But it can be used to control any 5v PWM fan. Or as an additional UART port (UART5 on CM4)

{: .warning }
Take care when wiring into this connector!

### UART connection (Smart Fan Unit)

On the Blade
Add to Config.txt

```bash
dtoverlay=uart5
```

Console:

```bash
sudo apt-get install cu
sudo chmod 666 /dev/ttyAMA1
sudo cu -l /dev/ttyAMA1 -s 115200
```

Fan Unit code:

[https://github.com/merocle/FanUnit](https://github.com/merocle/FanUnit){:target="_blank"}

{: .highlight-title }

> Notes:
>
> to close **cu** session:
> ```bash
> ~.
> ```
> to check if session in the background (in case “**cu: /dev/ttyAMA1: Line in use**” error):
> ```bash
> jobs -l
> ```
> to return to current opened session:
> ```bash
> fg
> ```

### PWM fan (non-smart Fan Unit)

When using a dumb Fan Unit the fan is controlled from the left blade in the pair

Examples:

```bash
wget https://raw.githubusercontent.com/DriftKingTW/Raspberry-Pi-PWM-Fan-Control/master/read_fan_speed.py
```

{: .important }
>You need to change in the script:
>**TACH = 13**

Run the script:

```bash
python read_fan_speed.py
```

Fan Control example:
```bash
wget https://raw.githubusercontent.com/DriftKingTW/Raspberry-Pi-PWM-Fan-Control/master/fan_control.py
python fan_control.py
```

{: .important }
>You need to change in the script:
>**FAN_PIN = 12**

to run the script in the background quickly, run
```bash
nohup python fan_control.py
```
Links:
[https://blog.driftking.tw/](https://blog.driftking.tw/en/2019/11/Using-Raspberry-Pi-to-Control-a-PWM-Fan-and-Monitor-its-Speed/){:target="_blank"} 