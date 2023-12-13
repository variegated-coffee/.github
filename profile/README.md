## Hi there 👋

[![Discord Shield](https://discordapp.com/api/guilds/1178966366523506709/widget.png?style=shield)](https://discord.gg/gn9aGHAc3U)

Do you have a Lelit espresso machine? Are you a bit of a nerd, both of coffee and hardware? Then this might be for you.

I'm creating open source hardware, firmware, and software for Lelit espresso machines. The [Open LCC main board](https://github.com/open-lcc/open-lcc-board) replaces the stock LCC board, and should (at least in theory) work on anything that has an LCC, though right now the only firmware is for the Bianca. It has an RP2040 for control, and an ESP32-S3 for Wi-fi and driving the screen (choose between a 128x64 px monochrome OLED like the original LCC, or a high-res color TFT).

*Important note*

Considering this project makes things that plugs in to an expensive machine it bears to mention: Anything you do with this, you do at your own risk. Components have been fried already during the course of this project. Your espresso machine uses both line voltage power, high pressured hot water, steam and other dangerous components. There is a risk of both damaging the machine, personal injury and property damage, the liability for which you assume yourself. Installing any of the hardware into your espresso machine presumably voids its warranty. The hardware is not certified by anybody, and the firmware is beta quality at best.

## Sounds great, what does it actually do?

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
* No more fiddling with settings menus, all settings are available through HTTP or Home Aassistant

I'm also working on or seriously considering the following:

* Using pressure sensors and scales in routines
* Stepped routines (i.e. manually cycling through routine steps, like on e.g. a Synesso)
* Upload shot profiles to Visualizer.coffee
* Ability to trigger/cancel a heat-up
* Steam only mode (i.e. brew boiler off)
* Standby mode (i.e. both boilers off, but controller on, not to be confused with Bianca V3 standby mode, since this mode is actually useful)

## Get involved

Interested in getting involved? Excellent! You'll likely need to start by having some hardware manufactured. Head off to the [Open LCC main board](https://github.com/open-lcc/open-lcc-board) repo. Not ready to manufacture some hardware, but still want to chat? [Join the Discord!](https://discord.gg/gn9aGHAc3U)

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->
