## Hi there 👋

[![Discord Shield](https://discordapp.com/api/guilds/1178966366523506709/widget.png?style=shield)](https://discord.gg/gn9aGHAc3U)

We're making open source hardware, firmware and software for espresso machines.                                                                                

## Active projects

* [APEC SoM](https://github.com/variegated-coffee/apec-som) - Short for All-Purpose Espresso Controller - System on Module - a module containing pretty much everything you need
to build a modern espresso machine controller
* [APEC Carrier for LM GS3](https://github.com/variegated-coffee/apec-carrier-lm-gs3) - An APEC SoM Carrier board designed for a La Marzocco GS3, compatible with gear pumps,
pressure sensors, proportional solenoids, load cells and more
* [APEC LM GS3 HMI module](https://github.com/variegated-coffee/apec-lm-gs3-hmi-module) - A replacement for the stock buttons and display of the La Marzocco GS3 with a nice big
TFT and RGB LEDs
* [Femtoprobe](https://github.com/variegated-coffee/femtoprobe) - An ultra-compact SWD and UART debug probe designed for ease of integration with the APEC SoM.
* [Open LCC Main Board](https://github.com/open-lcc/open-lcc-board) - A replacement for the Lelit LCC
* [Gravity](https://github.com/variegated-coffee/gravity) - A scale made for integration - by wire or without

### Get involved

Interested in getting involved? Excellent! The best way to get acquianted with the project at the moment is to [join the Discord!](https://discord.gg/gn9aGHAc3U)

### APEC SoM

Want to build a controller for an espresso machine, but would rather not start from a blank schematic? Then this might be for you.

The [APEC SoM](https://github.com/variegated-coffee/apec-som) puts the hard parts of an espresso machine controller on one small module: a 104-pin castellated board on a 1.27 mm
pitch. It's meant to sit on a machine-specific carrier board, which holds the connectors, FETs and passives that suit that machine. The SoM does the rest.

#### What's on it?

* An RP2350B microcontroller with 8 MB of program flash, 8 MB of settings flash and 8 MB of PSRAM
* An ESP32-C6 for Wi-Fi, Bluetooth, Zigbee and Thread (U.FL connector, so bring your own antenna)
* A TI ADS124S08 24-bit ADC for RTDs, pressure transducers and other precision analog inputs
* A TI FDC1004 capacitance-to-digital converter for level sensing in tanks and boilers
* A 4-port USB 2.0 hub. The RP2350B and the ESP32-C6 get one port each, and the other two are free for the carrier. Put a
[Femtoprobe](https://github.com/variegated-coffee/femtoprobe) on one of them, and a single USB cable gives you both microcontrollers, the ESP32's serial console and an SWD
debugger for the RP2350
* Its own power supplies: feed it 6–17 V and it makes 3.3 V, 5 V, a separate quiet 5 V rail for analog circuits, and a 6 V rail
* The ESP32-C6 can reset the RP2350, put it in its USB bootloader, or load code into it over the RP2350's UART boot interface

The KiCad symbol and footprints for carrier boards are included, in SMD, through-hole, SMD+THT and FlexyPin variants, under the same permissive licence as the rest of the design.
The [engineering notes](https://github.com/variegated-coffee/apec-som/blob/main/ENGINEERING-NOTES.md) cover what a carrier designer or firmware author needs to know.

### APEC Carrier for LM GS3

Do you have a La Marzocco GS3? Would you like to give it a gear pump, proportional solenoids or load cells, and run all of it on your own firmware? Or do you just have a broken control board, and want other options than to buy a new stock board? Then this might be for you.

The [APEC Carrier for LM GS3](https://github.com/variegated-coffee/apec-carrier-lm-gs3) replaces the GS3's control board. It fits the machine's existing mains, sensor and actuator wiring, and an APEC SoM provides the brains. Pair it with the [APEC LM GS3 HMI module](https://github.com/variegated-coffee/apec-lm-gs3-hmi-module) for a big TFT and RGB-lit buttons in the original display housing.

*Important note*
This board switches line voltage, and it goes inside a machine full of pressurised hot water and steam. Anything you do with it, you do at your own risk. It isn't a safety component: the machine's thermal cutouts, pressure relief and fuses must stay in place and work independently of it. It hasn't been tested or certified by anybody, and the project isn't affiliated with or endorsed by La Marzocco.

#### What's on it?

* The mains side, on a 13-position terminal block: relays for the group, fill and tea solenoids, a 16 A relay for the stock rotary pump, an on-board fuse, varistors on every
switched output, and a 12 V, 10 W AC/DC module for the low-voltage side
* SSR control outputs for the brew and service boilers
* An isolated 24 V section, fed from an external 24 V supply, with two outputs for proportional solenoids (steam and hot water) and a connector for an FG304 gear pump with speed, direction and tacho signals
* Two RTD inputs (PT1000, ratiometric) and two pressure transducer inputs (0.5–4.5 V), on the SoM's 24-bit ADC
* Two load cell inputs on a dedicated 24-bit ADC (NAU7802), so a scale can live inside the machine
* Capacitive level sensing for the tank and the boiler, plus inputs for a flow meter, the paddle switch and a potentiometer
* Display connectors for EyeSPI: an 18-pin FFC connector and a 2×10 IDC header (EyeDC-SPI)
* Two Qwiic connectors, an RTC with a backup battery and a microSD slot
* A UART connector that's pin compatible with the LM IoT module (not that you'd necessarily need one)
* USB-C for programming and debugging. The board runs from USB alone, so you can develop on the bench without mains
* An SWD header, a Femtoprobe footprint, and status LEDs for every output and power rail

### Open LCC Main Board

Do you have a Lelit espresso machine? Are you a bit of a nerd, both of coffee and hardware? Then this might be for you.

The [Open LCC main board](https://github.com/open-lcc/open-lcc-board) replaces the stock LCC board, and should (at least in theory) work on anything that has an LCC, though right now the only firmware is for the Bianca. It has an RP2040 for control, and an ESP32-S3 for Wi-fi and driving the screen (choose between a 128x64 px monochrome OLED like the original LCC, or a high-res color TFT).

*Important note*

Considering this project makes things that plugs in to an expensive machine it bears to mention: Anything you do with this, you do at your own risk. Components have been fried already during the course of this project. Your espresso machine uses both line voltage power, high pressured hot water, steam and other dangerous components. There is a risk of both damaging the machine, personal injury and property damage, the liability for which you assume yourself. Installing any of the hardware into your espresso machine presumably voids its warranty. The hardware is not certified by anybody, and the firmware is beta quality at best.

#### Sounds great, what does it actually do?

Whatever your imagination wants it to do, it's open source! 🌈

In all seriousness, here are some nice features of the [RP2040](https://github.com/open-lcc/rp2040-bianca) and [ESP32-S3](https://github.com/open-lcc/esphome-bianca) Bianca firmwares:

* Most of the things you can do with the stock V3 LCC
  * Includes the new faster heat-up routine
* Programmable, state machine based routines (right now only by defining them in code)
* Line pressure preinfusion (if you have a V3 Bianca, or you have rewired your V1/V2 water line solenoid to be separately controlled by control board), for those of us who have our machine hooked up to a tap or flojet
* Integration with the Pressensor Bluetooth Pressure Transducer
* Integration with Acaia scales (right now just the older, pre-Pyxis style scales)
* A nice graph view where you can see your shot graph directly on the LCC screen
* You can add additional temperature sensors; I have sensors on the E61 group inlet and the E61 group outlet (of course adding group temperature sensor is the most useful one, but A) it takes up the slot used by the pressure transducer, and B) it does not look good, given that it's wired, but it's useful to be able to swap it in occasionally)
* Integration into Home Assistant (ESP32-S3 firmware is based on ESPHome)
* No more fiddling with settings menus, all settings are available through HTTP or Home Assistant

We're also working on or seriously considering the following:

* Using pressure sensors and scales in routines
* Stepped routines (i.e. manually cycling through routine steps, like on e.g. a Synesso)
* Upload shot profiles to Visualizer.coffee
* Ability to trigger/cancel a heat-up
* Steam only mode (i.e. brew boiler off)
* Standby mode (i.e. both boilers off, but controller on, not to be confused with Bianca V3 standby mode, since this mode is actually useful)
