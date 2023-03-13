---
title: Ethernet with PoE
layout: page
parent: Main Features (Basic Blade)
permalink: "/main-features/ethernet/"
nav_order: 3
---

# Ethernet with PoE

The Compute Blade features a Gigabit Ethernet port that supports IEEE 802.3at (PoE+) and 802.3af (PoE).

## Power Consumption

Power consumption will vary based on load, accessories connected, the power requirements of any devices installed in the M.2 slot, whether or not the CM4 is overlocked, etc.

A compute blade with a CM4 overlocked to 2GHz and a normal NVMe SSD consumes ~7W under load. Normal operation may range from 3W to 17W.

A cluster of 40 blades running CI/CD tasks in a production environment consumes 260-280W, with 20 blades @ 1.8GHz and 20 blades overclocked to 2GHz.

## Cost

The cost to run a blade will depend on the power consumption considerations noted above and your local utility provider's rates. Some providers will vary the cost of electricity over the course of a day (peak vs. non-peak), which can further complicate the equation.

You can use an [energy cost calculator](https://www.rapidtables.com/calc/electric/energy-cost-calculator.html) to figure out kWh per day, month, or year, then mulitply that by your local utility provider's rates to determine the total cost to run a blade.

Examples: 

If a blade consumes 10W and runs 24 hours a day, that's 0.24 kWh/d. A fully-populated 19" rack mount shelf with 20 blades would consume 4.8 kWh/d.

* USD: At $0.20 per kWh, a blade would cost $0.048/d, or $0.96/d for a full shelf.
* EUR: At €0.19 per kWh, a blade would cost €0.046/d, or €0.82/d for a full shelf.

## PoE Modules

Different Compute Blade revisions use different PoE modules. See the table below.

| Version           | PoE Module                                        | Volts | Watts (Peak) | PoE Support                    | Classification               |
|:------------------|:--------------------------------------------------|:------|:-------------|:-------------------------------|:-----------------------------|
| RC2               | [Silvertel Ag5305](https://silvertel.com/ag5300/) | 5V    | 20W (22W)    | IEEE 802.3af, 802.3at          | Type 2, Class 4 <sup>2</sup> |
| v1.0 <sup>1</sup> | [Silvertel Ag5405](https://silvertel.com/ag5400/) | 5V    | 25.5W (30W)  | IEEE 802.3af, 802.3at, 802.3bt | Type 2, Class 4 <sup>3</sup> |

<sup>1</sup> _Unconfirmed. This module may or may not be used in v1.0. Once confirmed, this document will be updated._ 

<sup>2</sup> _"The Ag5300 classification is fixed at Class 4, this means that an IEEE802.3at Type 1 or an IEEE802.3af PSE will default to Class 0. However an IEEE802.3at or IEEE802.3bt PSE will recognise the Class 4 as a Type 2 PD." ([source](https://silvertel.com/images/datasheets/Ag5300-datasheet-smallest-30W-Power-Over-Ethernet-Plus-Module-PoEplusPD.pdf))_

<sup>3</sup> _"The Ag5400 is a fixed Type 2 - Class 4 PD requesting 30W of power from a compliant IEEE802.3 Type 2 or greater PSE by displaying the correct class pulses shown in Table 3 below. If the Ag5400 is connected to a Type 1 PSE, the PSE will not recognise the Class 4 request from the Ag5400 and default to a Class 3 power level device and supply 15.4W." ([source](https://silvertel.com/images/datasheets/Ag5400-datasheet-high%20Efficiency-30W-Power-Over-Ethernet-Plus-Module-PoE+PD.pdf))_

## PoE Standards

This is not meant to be an exhaustive reference. For detailed information, see [Power over Ethernet](https://en.wikipedia.org/wiki/Power_over_Ethernet).

| Standard                                                              | Common Name  | Type | PD     | Max. PSE | 
|:----------------------------------------------------------------------|:-------------|:-----|:-------|:---------|
| [IEEE 802.3af](https://standards.ieee.org/ieee/802.3af/1090/)         | PoE          | 1    | 12.95W | 15.4W    |
| [IEEE 802.3at](https://standards.ieee.org/standard/802_3at-2009.html) | PoE+         | 2    | 25.5W  | 30.0W    |
| [IEEE 802.3bt](https://standards.ieee.org/ieee/802.3bt/6749/)         | PoE++, 4PPoE | 3    | 51W    | 60W      |
| [IEEE 802.3bt](https://standards.ieee.org/ieee/802.3bt/6749/)         | PoE++, 4PPoE | 4    | 71.3W  | 100W     |

Use Cat5 cabling or better. Cat3 can be used in certain low-power situations, but most should not find themselves in a situation where Cat3 is needed.

## Switch Recommendation

A switch that supports IEEE 802.3at (PoE+) is recommended. However, IEEE 802.3af (PoE) is sufficient for a blade with a CM4 @ 1.8GHz and a standard NVMe SSD. Future M.2 modules (Coral, RAID, etc.) will require more power; 802.3af may not be adequate.

### Considerations

* PoE standard(s) supported.
* PoE budget.<sup>1</sup>
* Port count.
* Port speed.
* Form factor.

<sup>1</sup> _Note the switch's PSU, switch power consumption, and power available to PoE. Switches are not always capable of providing full power to all available switch ports. For example, a switch with a 500W PSU, with 50W switch power consumption, has a 450W PoE budget. That allows 26.25W per port for a 24-port switch, but only 9.375W for a 48-port switch._ 

### Switches In Use

A list of switches that Compute Blade users have successfully used to connect and power Compute Blades. For reference only.

| Switch                                                                     | Part No.       | Ports                          | PoE                |
|:---------------------------------------------------------------------------|:---------------|:-------------------------------|:-------------------|
| [Ubiquiti Switch Pro 24 PoE](https://store.ui.com/products/usw-pro-24-poe) | USW-PRO-24-POE | 24x 1GbE RJ45, 2x 1/10GbE SFP+ | 16x PoE+, 8x PoE++ |