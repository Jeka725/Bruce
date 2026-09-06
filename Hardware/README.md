# Hardware

This directory contains all hardware reference files for the Smoochie Board.

## Contents

```
hardware/
├── schematics/
│   └── BRUCE_Smoochie_Board_Full_Schematics.jpg   ← full wiring diagram
├── pinout/
│   └── esp32s3_pinout.md                          ← all GPIO assignments
├── bom/
│   └── bill_of_materials.csv                      ← full parts list
└── README.md
```

## Quick Reference

- **Microcontroller:** ESP32-S3 WROOM-1 N16R8 (16MB Flash / 8MB PSRAM)
- **SPI Bus:** CC1101, nRF24L01, TFT Display
- **I2C Bus:** PN532 (NFC/RFID)
- **UART:** NEO-6M GPS
- **Power:** 3.7V 2000mAh Li-ion → DC-DC boost to 5V → ESP32-S3 internal 3.3V regulator

## Building Your Own

1. Source all components from the BOM
2. Set the DC-DC boost converter output to 5V before connecting any modules
3. Set the PN532 DIP switch to I2C mode before wiring
4. Flash Bruce firmware with the pin assignments from `esp32s3_pinout.md`
5. Verify each module independently before full assembly
