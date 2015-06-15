
# Overview #

This is how the tracker looks like:

![Shield](https://github.com/trackuino/trackuino/wiki/img/trackuino-2.2-640px.jpg)

# Building the tracker #

The latest version of the Trackuino shield is 2.2.

Use the `Download ZIP` button to get the schematic / pcb files.

You can use the PCB fab house of your preference to have it manufactured. I have been using [iteadstudio.com's PCB prototyping service](http://iteadstudio.com) with success so far. The gerber files included in the zip were generated for iteadstudio.

Here is the bill of materials:

| Label | Qty | Component | Provider |
|:------|:----|:----------|:---------|
| C1, C2 | 2 | 10 µF | [Mouser](http://www.mouser.es/Search/ProductDetail.aspx?R=TAP106K016SCSvirtualkey58110000virtualkey581-TAP106K016SCS) |
| GPS | 1 | Venus 638FLPx | [Sparkfun](https://www.sparkfun.com/products/11058?) (check for local distributors if you want to avoid customs) |
| GPS | 1 | Female headers | [Mouser](http://www.mouser.es/ProductDetail/3M-Electronic-Solutions-Division/929974-01-20-RK/?qs=sGAEpiMZZMs%252bGHln7q6pm%252bCiuHjnbsudNOf3L7d921I%3d), or [Banggood](http://www.banggood.com/100Pcs-40Pin-2_54mm-Female-Header-Connector-Socket-For-DIY-Arduino-p-945506.html) for a lifetime supply. Cut them to desired size. |
| IC2 | 1 | 3.3V LDO regulator | [Mouser](http://www.mouser.es/Search/ProductDetail.aspx?R=AP1117E33G-13virtualkey62110000virtualkey621-AP1117E33G-13) |
| IC3, IC4, IC5 | 3 | 3-5.5V buffer | [Mouser](http://www.mouser.es/Search/ProductDetail.aspx?R=M74VHC1GT125DT1Gvirtualkey58410000virtualkey863-M74VHC1GT125DT1G) |
| J1, J2, J3, J4 | 1 set | Arduino 6, 8 pin male-female headers | [Dealextreme](http://www.dx.com/p/2-mm-pitch-8-pin-male-to-female-pin-headers-for-arduino-5-pcs-152201) + [Dealextreme](http://www.dx.com/p/2-5mm-pitch-6-pin-male-to-female-pin-headers-for-arduino-5-pcs-152192) (5 sets) or [Dealextreme](http://www.dx.com/p/6pin-8pin-10pin-2-3pin-pin-header-set-for-arduino-expansion-board-black-389423) (1 set)| 
| J5 | 1 | Pin header | Searching for pin headers in Mouser is a PITA. I suggest buying from [Dealextrme](http://www.dx.com/p/2-54mm-1x40-pin-breakaway-straight-male-header-10-piece-pack-144191#.VX8i2c6-RF8) or [Banggood](http://www.banggood.com/10-Pcs-40-Pin-2_54mm-Single-Row-Male-Pin-Header-Strip-For-Arduino-p-918427.html) where you get a lot more for a fraction the price |
| M2 | 1 | Radiometrix HX1 | [Radiometrix, 144.800 MHz](http://radiometrix.com/content/hx1) for Europe. The US distributor of the 144.390 MHz version is [Lemos International](http://www.lemosint.com/) |
| Q1 | 1 | IRFML8244TRPBF N-channel MOSFET | [Mouser](http://www.mouser.es/ProductDetail/International-Rectifier/IRFML8244TRPBF/?qs=%2fha2pyFaduiBVZ08reLy232NPPRTvJ0C96rIvgfREek%3d) |
| R1 | 1 | 10K | [Mouser](http://www.mouser.es/Search/ProductDetail.aspx?R=CR1206-FX-1002ELFvirtualkey65210000virtualkey652-CR1206FX-1002ELF) |
| R2 | 1 | 3K3 | [Mouser](https://www.mouser.es/Search/ProductDetail.aspx?R=CR1206-FX-3301ELFvirtualkey65210000virtualkey652-CR1206FX-3301ELF) |
| R3 | 1 | 1K | [Mouser](https://www.mouser.es/Search/ProductDetail.aspx?R=CR1206-FX-1001ELFvirtualkey65210000virtualkey652-CR1206FX-1001ELF) |
| S1 | 1 | Pushbutton | [Mouser](http://www.mouser.es/Search/ProductDetail.aspx?R=1301.9303virtualkey69300000virtualkey693-1301.9303), or lifetime supply from [Dealextreme](http://www.dx.com/p/jiahui-a054-plastic-phosphor-bronze-12a-4pin-switch-black-silver-15-pcs-257124) | 
| U1 | 1 (internal) + 1 (external) | LM60 thermometer | [Mouser](https://www.mouser.es/Search/ProductDetail.aspx?R=LM60CIZ%2fNOPBvirtualkey59500000virtualkey926-LM60CIZ%2fNOPB) |
| X1 | 1 | Female SMA connector | [Mouser](https://www.mouser.es/Search/ProductDetail.aspx?R=961A514virtualkey67800000virtualkey678-961A514), [Dealextreme](http://www.dx.com/p/gold-plating-sma-female-pcb-end-launch-mount-connectors-golden-5-pcs-149787), [Banggood](http://www.banggood.com/Golden-Copper-SMA-Female-Jack-Center-PCB-Solder-RF-Connector-p-924929.html) |
| X2, X4 | 2 | 2-pin terminal block (screw clamp) | [Mouser](http://www.mouser.es/Search/ProductDetail.aspx?R=1935161virtualkey65100000virtualkey651-1935161), [Banggood](http://www.banggood.com/50pcs-2pins-Printed-Circuit-Board-Connector-Block-Screw-Terminals-p-943634.html), probably easy to find on Aliexpress, Dealextreme, etc. |
| X3 | 1 | 3-pin terminal block (screw clamp) | [Mouser](http://www.mouser.es/Search/ProductDetail.aspx?R=1935174virtualkey65100000virtualkey651-1935174), [Dealextreme](http://www.dx.com/p/3-pin-screw-terminal-block-connectors-20-piece-pack-122491), ... (same as above) |

In addition to the above, you need:

  * [GPS antenna](http://dx.com/p/digital-gps-antenna-1575mhz-f-cable-5303) from Dealextreme. Mouser also carries SMA GPS antennas if you think DX is too slow. Make sure the connector is the SMA male type. Read the [SMA-connectors](https://github.com/trackuino/shield/wiki/SMA-connectors) page for clarification on the SMA/RPSMA/male/female nomenclature. Even though the DX description says "F cable", it's actually a male SMA, but doublecheck before buying.
  * VHF (144 MHz) antenna. A DIY 1/4 wave groundplane (with radials) is the most effective.

# Power #

There are 3 ways to power the tracker. In either case, the recommended voltage is 7..12 VDC:

  1. Using the Arduino barrel jack, or...
  1. Using the VIN and GND clamp terminals (next to the GPS module).
  1. Using a USB cable plugged to a host computer. This will work because of the reverse current diode built in the 5V regulator, which will provide enough voltage to power the shield's 3.3V regulator.

Power usage for a 7.5 VDC reference voltage is:

| Status | Current |
|:--------------------|:-------|
| Waiting for GPS fix | 120 mA |
| Normal operation (idle) | 70 mA |
| Normal operation (HX1 transmitting) | 200 mA |

# Buzzer #

There are two kinds of buzzers:

  * Active (aka DC) buzzers and
  * Passive (aka AC) buzzers

The fundamental difference is that active buzzers take a direct current (DC) voltage whereas passive buzzers are driven by a square wave. DC buzzers have an internal oscillator that translates DC into a fixed-frequency square wave, which is then used to drive the piezoelectric membrane. An AC buzzer, on the other hand, needs that square wave to be generated externally and thus its frequency can be controlled.

The Trackuino shield can use both kinds of buzzers:

  * If you use an **active (DC)** buzzer:
    * Do **not** solder `R3`
    * In config.h, set BUZZER\_TYPE to 0.
    * DC buzzers have a fixed frequency, so BUZZER\_FREQ won't matter.
  * If you use a **passive (AC)** buzzer:
    * **Do** solder `R3`. Piezo buzzers behave as capacitors and when the fet is off they need a path to discharge and relax. Because of this bleeder resistor, the buzzer won't sound as loud as if it was driven by a push-pull buffer, but it keeps things simpler.
    * In config.h, set BUZZER\_TYPE to 1.
    * Set BUZZER\_FREQ to the desired frequency in Hertz.

# What's with the jumpers? #

## J5 ##

When shorted, this jumper connects the Arduino TX pin with the GPS RX pin so that the MCU can send commands to the GPS, but then you can't print any debug information out the serial port and into the Arduino IDE's console.

When open, you can print debug info from the firmware and it will be displayed on the Arduino IDE's console, but you can't send commands to the GPS.

I suggest soldering a two pin male header on J5, or just **leaving it unpopulated**, since the GPS doesn't need any special command from the firmware to operate normally, whereas debug information can be useful when hacking or diagnosing the firmware.

## J6, J7, J8 ##

Since shield version 2.1, the board can talk to both 5V and 3.3V microcontrollers, so you can plug the board into a 5V Arduino as well as 3.3V compatible devboards like the Chipkit Uno32. The shield uses 74\*125 buffers that work as 3.3/5V level converters. The HX1 module uses 5V logic and the Venus GPS uses 3.3V logic, so no matter what the logic of your MCU is, some conversion needs to be done:

  * If your MCU is 5V (Arduino Duemilanove, Uno): IC4 needs to be soldered and J6, J8 need to be shorted. IC4 provides the 5->3.3V downconversion for the GPS.
  * If your MCU is 3.3V (Chipkit Uno32): IC3, IC5 need to be soldered and J7 needs to be shorted. IC3 and IC5 provide the 3.3V->5V conversion for the two HX1 inputs.

I suggest to solder all three buffers (IC3, IC4 and IC5) and none of the bridges (J6, J7, J8), then you will have a board that is compatible with **both** 5V and 3.3V logics.

# Caution #

Things you should pay special attention to:

  * First and foremost, do **not** turn on the tracker without a proper antenna!! Power not radiated by the HX1 will reflect back and cause overheating that might eventually fry the HX1 and/or the whole board.
  * Be careful when you plug the shield. It's relatively easy to misalign the headers and leave one or more pins outside the sockets.
  * If you use an external LM60, make sure it's connected properly. Here is the [LM60 datasheet](http://www.ti.com/lit/ds/symlink/lm60.pdf). For a quick test, you can spread out the pins of the chip and connect it directly to the terminal blocks, with its **flat side facing up**.

# Building the firmware #

The recommended version of the firmware is [Trackuino 1.51](https://github.com/trackuino/trackuino/tree/1.51). Check that page for downloading and building directions.

# Testing #

Refer to [Troubleshooting](Troubleshooting.md) if something doesn't work the way it should.
