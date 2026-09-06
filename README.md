<!--
  SEO keywords (for GitHub/Google indexing; keep near the top):
  ESP32-S3 pentest, wireless security deck, Bruce firmware, Flipper Zero alternative,
  CC1101 Sub-GHz, nRF24L01, PN532 NFC/RFID, IR transceiver, NEO-6M GPS,
  handheld wardriving, IoT security research, red team hardware, DIY pentest hardware.
-->

<div align="center">

# Bruce Smoochie: ESP32-S3 Wireless Pentest Deck

### A portable, battery-powered, multi-radio wireless security research platform
### Wi-Fi · BLE · Sub-GHz · 2.4 GHz IoT · IR · NFC/RFID · GPS, all in one handheld device

<img src="images/Bruce%20with%20white%20case.png" alt="Bruce Smoochie ESP32-S3 Wireless Pentest Deck: handheld device with antennas and IPS display" width="640" />

<br />

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Platform: ESP32-S3](https://img.shields.io/badge/Platform-ESP32--S3-red.svg)](https://www.espressif.com/en/products/socs/esp32-s3)
[![Firmware: Bruce](https://img.shields.io/badge/Firmware-Bruce-orange.svg)](https://github.com/pr3y/Bruce)
[![Made at: Pace University](https://img.shields.io/badge/Made%20at-Pace%20University-002856.svg)](https://www.pace.edu/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing)
[![Stars](https://img.shields.io/github/stars/arpitxp/esp32-bruce-wireless-pentest-deck?style=social)](https://github.com/arpitxp/esp32-bruce-wireless-pentest-deck/stargazers)

**[Features](#features) · [Hardware](#hardware) · [Gallery](#gallery) · [Build Your Own](#build-your-own) · [Capabilities](#capabilities) · [License](#license)**

</div>

---

## Overview

**Bruce Smoochie** is an open-source, ESP32-S3 powered handheld wireless pentest deck: a self-contained, battery-operated tool that consolidates **Wi-Fi, Bluetooth/BLE, Sub-GHz RF (CC1101), 2.4 GHz proprietary IoT (nRF24L01+PA/LNA), Infrared, NFC/RFID (PN532), and GPS (NEO-6M)** into a single pocketable device. It runs a customized build of the [Bruce firmware](https://github.com/pr3y/Bruce) and operates entirely off a Li-ion cell. No laptop, no tether, no network required.

Designed and built as a capstone research project at **Pace University (CYB691)**, the project's goal is to provide a transparent, reproducible, and educational alternative to closed-source commercial pentest devices. Every schematic, pinout, bill of materials, and firmware customization is published in this repository so anyone can build, study, or extend the device.

If the Flipper Zero, HackRF, and a wardriving rig had a hackable open-source cousin, this is it.

---

## Why Bruce Smoochie?

Most commercial all-in-one pentest tools ship as sealed black boxes. This project takes the opposite approach: a fully documented, **reproducible hardware + firmware stack** built on widely available modules, with every design decision explained.

- **Truly standalone.** Boots into a menu-driven UI on a 1.47" IPS TFT, powered by an 800 mAh Li-ion cell. No companion app, no serial tether.
- **Seven radios, one board.** Switch between Wi-Fi, BLE, Sub-GHz, 2.4 GHz IoT, IR, NFC/RFID, and GPS without rebooting.
- **Open hardware.** Full schematics, GPIO map, and bill of materials. Every module is off-the-shelf.
- **Open firmware.** Custom C++ extensions on top of the Bruce firmware, with multi-radio coordination across SPI, I²C, and UART buses.
- **Education-first.** Built to teach the fundamentals of IoT and wireless protocol security in a classroom or lab setting.

---

## Gallery

<table>
  <tr>
    <td align="center" width="50%">
      <img src="images/Bruce%20with%20white%20case.png" alt="Bruce Smoochie ESP32 pentest deck in finished 3D-printed enclosure" width="100%" /><br/>
      <sub><b>Finished build.</b> 3D-printed enclosure with CC1101 and nRF24 antennas exposed.</sub>
    </td>
    <td align="center" width="50%">
      <img src="images/portable.jpg" alt="Bruce Smoochie ESP32-S3 prototype showing Wi-Fi scanning menu on IPS display" width="100%" /><br/>
      <sub><b>Prototype.</b> Hand-wired protoboard running the Wi-Fi module on a 1.47" 172×320 IPS LCD.</sub>
    </td>
  </tr>
</table>

<div align="center">
  <img src="hardware/schematics/BRUCE%20Smoochie%20Board%20Full%20Schematics.jpg" alt="Full wiring schematic for the Bruce Smoochie ESP32-S3 wireless pentest deck" width="720" /><br/>
  <sub><b>Full schematic.</b> ESP32-S3 WROOM-1 with all seven radio modules, power stage, and SPI/I²C/UART assignments.</sub>
</div>

---

## Features

| Category | Capability |
|---|---|
| Wi-Fi (2.4 GHz) | SSID enumeration, RSSI monitoring, encryption detection (WEP/WPA/WPA2) |
| Bluetooth / BLE | Device discovery, advertising packet observation, basic fingerprinting |
| Sub-GHz RF | Signal capture & replay across 315 / 433 / 868 / 915 MHz via CC1101 |
| 2.4 GHz IoT | Packet capture & replay on proprietary low-power IoT links (nRF24L01+PA/LNA) |
| Infrared | Capture and replay of NEC, RC5, and related consumer IR protocols |
| NFC / RFID | MIFARE Classic 1K detection, ISO/IEC 14443-4 tag UID read via PN532 |
| GPS | NMEA logging, signal-to-location correlation for wardriving |
| UI | On-device menu on a 1.47" 172×320 IPS TFT with 5-way button nav |
| Power | 800 mAh Li-ion, TP4056 charging, ~2–3 hours active scanning |
| Storage | LittleFS on internal flash, no SD card required |

---

## Hardware

### Core

| Component | Details |
|---|---|
| MCU | **ESP32-S3 WROOM-1 N16R8** (dual-core Xtensa LX7, 16 MB Flash / 8 MB PSRAM) |
| Display | 1.47" IPS TFT, 172×320 RGB, ST7789 controller, SPI |
| Storage | LittleFS on internal flash |
| Battery | 3.7 V 800 mAh Li-ion with TP4056 charger |
| Power path | Li-ion → TP4056 → switch → DC-DC boost to 5 V → ESP32-S3 3.3 V LDO |
| Runtime | ~2–3 hours of active multi-radio scanning |

### Radios and Peripherals

| Module | Role | Bus | Frequency |
|---|---|---|---|
| ESP32-S3 (built-in) | Wi-Fi 802.11 b/g/n | Internal | 2.4 GHz |
| ESP32-S3 (built-in) | Bluetooth Classic / BLE | Internal | 2.4 GHz |
| **CC1101** | Sub-GHz transceiver | SPI | 315 / 433 / 868 / 915 MHz |
| **nRF24L01+PA/LNA** | Proprietary 2.4 GHz IoT | SPI | 2.4 GHz |
| **PN532** | NFC / RFID | I²C | 13.56 MHz |
| **NEO-6M** | GPS (NMEA) | UART | n/a |
| **TSOP38438 + KY-005** | IR RX / TX | GPIO | 38 kHz (carrier) |

Full wiring and GPIO-by-GPIO assignments live in [`hardware/pinout/README.md`](hardware/pinout/README.md). The complete schematic image is in [`hardware/schematics/`](hardware/schematics/), and the bill of materials (with part numbers and approximate prices) is in [`hardware/bill_of_materials/`](hardware/bill_of_materials/).

---

## System Architecture

The ESP32-S3 acts as the coordinator for every radio on the board, multiplexing access across three buses:

- **SPI bus:** CC1101, nRF24L01, TFT display (independent chip-selects)
- **I²C bus:** PN532 NFC/RFID module
- **UART:** NEO-6M GPS receiver
- **Internal RF:** Wi-Fi and BLE via the ESP32-S3 radio

Power is sourced from a single Li-ion cell, routed through a TP4056 charger and a mini DC-DC boost converter to generate a stable 5 V rail. 3.3 V is derived on-board from the ESP32-S3. Smoothing capacitors (10 µF + 100 nF) sit across the 5 V rail to stabilize switching noise during multi-radio scans.

The firmware coordinates all modules through an abstraction layer that lets you switch protocols from the menu without rebooting, and logs every captured signal to LittleFS on the internal flash so no SD card is needed.

---

## Capabilities

### Wi-Fi
Real-time 2.4 GHz network scanning, SSID enumeration, encryption type identification (WEP / WPA / WPA2), and live RSSI tracking. Useful for authorized site surveys and classroom demos of weak encryption practices.

### Bluetooth / BLE
Discovery of nearby Classic and BLE devices, observation of advertising packets, and basic protocol-level fingerprinting. A starting point for BLE security research.

### Sub-GHz RF (CC1101)
Capture and replay of signals on the 315 / 433 / 868 / 915 MHz bands. Ideal for demonstrating replay vulnerabilities in unencrypted key fobs, wireless doorbells, garage remotes, and legacy industrial sensors in a controlled lab environment.

### 2.4 GHz IoT (nRF24L01+PA/LNA)
Capture and replay on proprietary low-power IoT links (smart plugs, wireless peripherals, some toys and remotes). Demonstrates why rolling-code and authenticated protocols matter.

### Infrared
Capture and replay IR commands from consumer remotes (NEC, RC5, and related protocols) to show how trivially unauthenticated IR control can be spoofed.

### NFC / RFID (PN532)
UID extraction from ISO/IEC 14443-4 tags, MIFARE Classic 1K detection, and display of card data on the IPS screen. A practical teaching tool for access-badge security.

### GPS Logging (NEO-6M)
NMEA logging with ceramic patch antenna, typical cold-start fix in 20–40 seconds outdoors. Pair with Wi-Fi scans for wardriving and signal-to-location correlation; export logs for mapping tools.

---

## Tested Results

| Test | Result |
|---|---|
| MIFARE Classic 1K RFID UID read | ✅ UID displayed on-screen within 4 cm range |
| GPS cold-start satellite lock (outdoors) | ✅ Stable fix in 20–40 s |
| Battery runtime, active multi-radio scan | ✅ ~2–3 h on 800 mAh cell |
| nRF24L01 packet capture | ✅ Validated |
| CC1101 Sub-GHz init + detection | ✅ Confirmed across four bands |
| IR capture + replay | ✅ Successful round-trip on NEC protocol |
| Wi-Fi scan + live UI on battery | ✅ Stable, no tethering required |

---

## Repository Structure

```
esp32-bruce-wireless-pentest-deck/
├── firmware/                     # Bruce firmware build + custom extensions
│   └── Bruce-smoochiee-board.bin
├── hardware/
│   ├── schematics/               # Full wiring diagram (JPG)
│   ├── pinout/                   # GPIO-by-GPIO assignments (Markdown)
│   └── bill_of_materials/        # Parts list (XLSX)
├── docs/                         # Capstone report + presentation
├── images/                       # Device photography
├── LICENSE
└── README.md
```

---

## Build Your Own

1. **Source the parts.** The full bill of materials is in [`hardware/bill_of_materials/`](hardware/bill_of_materials/). Every module is off-the-shelf.
2. **Pre-set the boost converter.** Adjust the mini DC-DC output to exactly **5 V** before wiring any modules.
3. **Configure the PN532.** Set its on-board DIP switch to **I²C mode** before connecting SDA/SCL.
4. **Wire to the pinout.** Follow [`hardware/pinout/README.md`](hardware/pinout/README.md). Every GPIO is mapped and color-coded.
5. **Flash the firmware.** Use the provided `Bruce-smoochiee-board.bin` in [`firmware/`](firmware/), or build from source following the upstream [Bruce firmware](https://github.com/pr3y/Bruce) instructions.
6. **Bench-test each module** (Wi-Fi → BLE → CC1101 → nRF24 → IR → PN532 → GPS) before final assembly in the enclosure.

---

## Usage

1. Power on. The device boots into the Bruce firmware menu on battery.
2. Use the 5-way navigation to select a protocol (Wi-Fi, BLE, Sub-GHz, 2.4 GHz IoT, IR, NFC, GPS).
3. Observe live wireless activity on the IPS display.
4. Capture or log signals as needed. Events are persisted to LittleFS.
5. Offload logs via USB for analysis and mapping.

---

## Intended Use Cases

- Wireless security education and classroom lab exercises
- Authorized penetration testing and red-team simulations
- IoT protocol vulnerability research
- Pre-deployment wireless infrastructure assessment
- Wardriving and RF signal mapping
- Hands-on training for cybersecurity students and practitioners

---

## Ethical Use & Legal Notice

This device is intended **strictly** for:

- Authorized security testing with explicit written permission
- Educational and research purposes in controlled environments
- Legal, documented penetration-testing engagements

**All wireless testing must be conducted with explicit permission from the network or device owner.** Unauthorized interception, decoding, or replay of radio signals may violate local, state, and federal laws including, but not limited to, the U.S. Computer Fraud and Abuse Act (CFAA), the Wiretap Act, and analogous statutes in other jurisdictions.

The authors assume **no responsibility** for misuse of this hardware or firmware. If you're not sure whether a test is legal, don't run it.

---

## Contributing

Pull requests are welcome. If you're porting the design to a different case, adding a protocol module, improving the firmware menu, or publishing a new test result, please open an issue first to discuss the change.

If this project saved you a weekend of schematic hunting, please **star the repo**. It helps others find the project and is the single most useful thing you can do to support open wireless-security research. ⭐

---

## Authors

**CYB691 Capstone, Pace University**

- [Arpit Dhameliya](https://github.com/arpitxp)

Built on top of the excellent [Bruce firmware by pr3y](https://github.com/pr3y/Bruce).

---

## Citation

If you reference this work in academic writing or derivative projects, please cite:

> Dhameliya, A. *Bruce Smoochie: A Standalone ESP32-S3 Wireless Pentest Deck.* CYB691 Capstone, Pace University, 2025. https://github.com/arpitxp/esp32-bruce-wireless-pentest-deck

---

## License

Released under the [MIT License](LICENSE). Hardware documentation and schematics are published under the same permissive terms. Build it, remix it, teach with it.

<div align="center">

---

**If you found this useful, a ⭐ on the repo goes a long way.**

[Report an issue](https://github.com/arpitxp/esp32-bruce-wireless-pentest-deck/issues) · [Fork the project](https://github.com/arpitxp/esp32-bruce-wireless-pentest-deck/fork) · [Discuss on GitHub](https://github.com/arpitxp/esp32-bruce-wireless-pentest-deck/discussions)

</div>
