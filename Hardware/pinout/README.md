# ESP32-S3 Pin Assignments — Smoochie Board

Double-verified point-to-point wiring for the BRUCE Smoochie Board.  
Derived from: `BRUCE_Smoochie_Board_Full_Schematics.jpg`  
Microcontroller: **ESP32-S3 WROOM-1 N16R8** (16MB Flash / 8MB PSRAM)

---

## Power System

| Connection | Detail |
|---|---|
| LiPo Battery `B+` / `B-` | → TP4056 Charger Module |
| Charger `OUT+` | → ON/OFF Switch |
| ON/OFF Switch | → Mini DC-DC Boost Converter `VIN` |
| Charger `OUT-` | → Mini DC-DC Boost Converter `GND` |
| DC-DC `5V OUT` | → ESP32 `5V` pin + IR Tx `VCC` |
| DC-DC `GND` | → Main GND bus (shared by all modules) |
| ESP32 `3.3V` | → Display, IR Rx, CC1101, GPS, nRF24, PN532, SD Card, pull-up resistors |

> Smoothing capacitors: 10µF and 100nF across 5V and GND lines.

---

## Display — ST7789 1.47" 172×320 SPI

| Module Pin | Wire Color | ESP32-S3 GPIO |
|---|---|---|
| GND | — | GND |
| VCC | — | 3.3V |
| SCL | Yellow | GPIO 12 |
| SDA | Blue | GPIO 11 |
| RES | Green | GPIO 10 |
| DC | Purple | GPIO 9 |
| CS | Pink | GPIO 46 |
| BLK | Light Blue | GPIO 3 |

---

## Navigation Buttons

> All signal lines pulled up to 3.3V via 10K resistors. Opposite pin → GND.

| Button | Wire Color | ESP32-S3 GPIO |
|---|---|---|
| UP | Purple | GPIO 14 |
| DOWN | Light Blue | GPIO 13 |
| LEFT | Green | GPIO 47 |
| RIGHT | Pink | GPIO 21 |
| SELECT | Yellow | GPIO 48 |

---

## IR Receiver — TSOP38438 (38kHz)

| Module Pin | ESP32-S3 GPIO |
|---|---|
| GND | GND |
| VCC | 3.3V |
| Signal | GPIO 4 |

## IR Transmitter — KY-005

| Module Pin | ESP32-S3 GPIO |
|---|---|
| GND | GND |
| VCC | **5V** (direct from DC-DC boost) |
| Signal | GPIO 5 |

---

## CC1101 — Sub-GHz Transceiver (SPI)

| Module Pin | Wire Color | ESP32-S3 GPIO |
|---|---|---|
| GND | — | GND |
| VCC | — | 3.3V |
| GDO0 | Light Blue | GPIO 16 |
| CSN | Yellow | GPIO 15 |
| SCK | Green | GPIO 18 |
| MOSI | Pink | GPIO 17 |
| MISO | Purple | GPIO 8 |
| GDO2 | Blue | GPIO 6 |

---

## NEO-6M GPS Module (UART)

| Module Pin | Wire Color | ESP32-S3 GPIO |
|---|---|---|
| VCC | — | 3.3V |
| GND | — | GND |
| RX | Purple | GPIO 39 |
| TX | Blue | GPIO 40 |

---

## nRF24L01+PA/LNA — 2.4 GHz Transceiver (SPI)

| Module Pin | Wire Color | ESP32-S3 GPIO |
|---|---|---|
| VCC | — | 3.3V |
| GND | — | GND |
| CE | Green | GPIO 7 |
| CSN | Yellow | GPIO 35 |
| SCK | Blue | GPIO 36 |
| MOSI | Pink | GPIO 37 |
| MISO | Purple | GPIO 38 |
| IRQ | — | Not Connected |

---

## PN532 — NFC / RFID (I2C)

> Set PN532 onboard DIP switch to I2C mode before wiring.

| Module Pin | Wire Color | ESP32-S3 GPIO |
|---|---|---|
| VCC | — | 3.3V |
| GND | — | GND |
| SDA | Blue | GPIO 2 |
| SCL | Yellow | GPIO 1 |

---

## SD Card Reader — XKTF N02 N (SPI)

> Dat2 and Dat1 have 10K pull-ups to 3.3V but no direct ESP32 connection.  
> SD Card is present in schematic but **not used in firmware** — LittleFS on internal flash is used instead.

| Module Pin | Wire Color | ESP32-S3 GPIO |
|---|---|---|
| Dat2 | — | 10K pull-up to 3.3V only |
| Dat3 / CS | Yellow | GPIO 42 |
| CMD / MOSI | Pink | GPIO 41 |
| VDD | — | 3.3V |
| CLK / SCK | Green | GPIO 20 |
| VSS / GND | — | GND |
| Dat0 / MISO | Purple | GPIO 19 |
| Dat1 | — | 10K pull-up to 3.3V only |
| CD | — | Not Connected |

---

## Full GPIO Map — Quick Reference

| GPIO | Function | Module |
|---|---|---|
| 1 | SCL | PN532 (I2C) |
| 2 | SDA | PN532 (I2C) |
| 3 | BLK | Display backlight |
| 4 | Signal | IR Receiver |
| 5 | Signal | IR Transmitter |
| 6 | GDO2 | CC1101 |
| 7 | CE | nRF24L01 |
| 8 | MISO | CC1101 |
| 9 | DC | Display |
| 10 | RES | Display |
| 11 | SDA / MOSI | Display (SPI) |
| 12 | SCL / SCK | Display (SPI) |
| 13 | DOWN | Button |
| 14 | UP | Button |
| 15 | CSN | CC1101 |
| 16 | GDO0 | CC1101 |
| 17 | MOSI | CC1101 |
| 18 | SCK | CC1101 |
| 19 | Dat0 / MISO | SD Card |
| 20 | CLK / SCK | SD Card |
| 21 | RIGHT | Button |
| 35 | CSN | nRF24L01 |
| 36 | SCK | nRF24L01 |
| 37 | MOSI | nRF24L01 |
| 38 | MISO | nRF24L01 |
| 39 | RX | GPS |
| 40 | TX | GPS |
| 41 | CMD / MOSI | SD Card |
| 42 | Dat3 / CS | SD Card |
| 46 | CS | Display |
| 47 | LEFT | Button |
| 48 | SELECT | Button |
