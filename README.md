# What's new #

Changes since [TrackuinoShield21](TrackuinoShield21.md):

  * Replaced Venus GPS 634FLPx (sparkfun #9133) with newer 638FLPx (sparkfun #11058). The unfortunate pinout reshuffling in the newer part makes version 2.2 of the tracker incompatible with the older part.
  * Eagle 6.x is required
  * Use Arduino's own 5V regulator
  * Replaced TO220 3.3V regulator with SMT + board sink
  * Added bleeder resistor for passive piezo speakers

# Overview #

This is how the tracker looks like:

![http://wiki.trackuino.googlecode.com/hg/img/trackuino-2.2-640px.jpg](http://wiki.trackuino.googlecode.com/hg/img/trackuino-2.2-640px.jpg)

# Building the tracker #

Download trackuino-shield-2.2.zip from the [downloads area](http://code.google.com/p/trackuino/downloads/list). You can use the PCB fab house of your preference to have it manufactured. I have been using [iteadstudio.com's PCB prototyping service](http://iteadstudio.com) with success so far. The gerber files included in the zip were generated for iteadstudio.

Here is the bill of materials:

| **Note:** Mouser has set minimum orders on some parts, like resistors and pin headers. You are forced to buy the full reel (5000) even if you want just a few resistors. If anyone is willing to find alternative sources and put a new BOM together, the contribution would be very welcome. Just drop a comment below |
|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

| **Update:** See comments below for user-contributed BOMs from alternative providers |
|:------------------------------------------------------------------------------------|

  * [Mouser BOM](http://mouser.com/ProjectManager/ProjectDetail.aspx?AccessID=511d111583) (includes 1 Arduino board, remove it if you have one already)
  * [Venus 638FLPx GPS](https://www.sparkfun.com/products/11058?) from Sparkfun (check for local distributors if you want to avoid customs)
  * [Radiometrix HX1, 144.800 MHz](http://radiometrix.com/content/hx1) for Europe. The US distributor of the 144.390 MHz version is [Lemos International](http://www.lemosint.com/).
  * [GPS antenna](http://dx.com/p/digital-gps-antenna-1575mhz-f-cable-5303) from Dealextreme. Mouser also carries SMA GPS antennas if you think DX is too slow. Make sure the connector is the SMA male type. Read the [SMAConnectors](SMAConnectors.md) page for clarification on the SMA/RPSMA/male/female nomenclature. Even though the DX description says "F cable", it's actually a male SMA, but doublecheck before buying.
  * VHF (144 MHz) antenna. A DIY 1/4 wave groundplane (with radials) is the most effective. Check [Antennas](Antennas.md) for ideas.

# Power #

There are 3 ways to power the tracker. In either case, the recommended voltage is 7..12 VDC:

  1. Using the Arduino barrel jack, or...
  1. Using the VIN and GND clamp terminals (next to the GPS module).
  1. Using a USB cable plugged to a host computer. This will work because of the reverse current diode built in the 5V regulator, which will provide enough voltage to power the shield's 3.3V regulator.

Power usage for a 7.5 VDC reference voltage is:

| Waiting for GPS fix | 120 mA |
|:--------------------|:-------|
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

The recommended version of the firmware is [TrackuinoFirmware15](TrackuinoFirmware15.md). Check that page for downloading and building directions.

# Testing #

Refer to [Troubleshooting](Troubleshooting.md) if something doesn't work the way it should.