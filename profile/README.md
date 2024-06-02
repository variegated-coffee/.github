## Hi there 👋

[![Discord Shield](https://discordapp.com/api/guilds/1178966366523506709/widget.png?style=shield)](https://discord.gg/gn9aGHAc3U)

We're making open source hardware, firmware and software for espresso machines.

* [Open LCC Main Board](https://github.com/open-lcc/open-lcc-board) - A replacement for the Lelit LCC
* [All-purpose Espresso Controller](https://github.com/open-lcc/all-purpose-espresso-controller) - A controller for any reasonably complicated espresso machine that fits in a Gicar 8.5 series enclosure
* [All-purpose Espresso Controller HV Board](https://github.com/open-lcc/all-purpose-espresso-controller-hv-board) - A mains voltage board with relays and an AC/DC converter
* [FG Filter Board](https://github.com/open-lcc/fg-filter) - A board allowing a Fluid-o-Tech FG200/300/400 series Gear Pump to be controlled by PWM

### What board do I need?

Enjoy this lovely flow chart!

[![Hardware selection flow chart](https://github.com/variegated-coffee/.github/blob/main/docs/flow_chart.png?raw=true)](https://github.com/variegated-coffee/.github/blob/main/docs/flow_chart.png?raw=true)

### Get involved

Interested in getting involved? Excellent! The best way to get acquianted with the project at the moment is to [join the Discord!](https://discord.gg/gn9aGHAc3U)

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

### All-purpose espresso controller

Do you have an espresso machine that's not from Lelit? Or do you have a Lelit machine but want to get in to some really exciting things, like gear pumps? Then the All-purpose Espresso Controller is (or rather will be) for you. 

This is a preliminary list of features:

* RP2040 MCU with 2 MB of QSPI program flash, and 2 MB of SPI settings flash
* ESP32-S3 MCU with 16 MB Flash and 8 MB PSRAM
* 12V, 5V, 5VA and 3V3 power domains, with TPS82130 buck converters for 5V and 3V3 (allowing up to 3A), and a TC2015-5.0 LDO for the 5VA power domain
* HMI device connector (compatible with both Open LCC and Nextion displays) with UART, one controllable 12V pin, one controllable 5/3.3 V pin, and one 5/3.3V supply pin
* 9x drain-to-ground N-ch MOSFETs supporting (for controlling things like SSRs)
* 4x P-ch MOSFET controlled 5V or 12V outputs (for things that need an actual 5V / 12V control signal)
* ADS124S08 12 channel 24-bit ΔΣ ADC with RC filters, usable for thermocouples, NTC thermistors, RTDs etc, as well as analog sensors such as pressure transducers.
* FDC1004 4 channel capacitance-to-digital converter, with all channels exposed. Useful for liquid level sensing.
* 13x 3V3 GPIOs, 2 of which can be configured as 3V3/5V outputs instead.
* QWIIC connectors for both RP2040 and ESP32-S3 for further expansion
* EyeSPI connector connected to ESP32-S3 for further expansion
* SD Card slot connected to the RP2040 for additional storage
* RP2040 USB programming interface and SWD debug header
* ESP32-S3 USB programming interface, JTAG debug header and ESP-DEBUG compatible UART header

The All-Purpose Espresso Controller isn't ready for prime time yet, but you should absolutely take a [look at the repository](https://github.com/open-lcc/all-purpose-espresso-controller), and [join the Discord](https://discord.gg/gn9aGHAc3U) if you're interested!
