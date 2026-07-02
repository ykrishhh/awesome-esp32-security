# Awesome ESP32 Security

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![GitHub stars](https://img.shields.io/github/stars/ykrishhh/awesome-esp32-security?style=social)](https://github.com/ykrishhh/awesome-esp32-security)
[![GitHub forks](https://img.shields.io/github/forks/ykrishhh/awesome-esp32-security?style=social)](https://github.com/ykrishhh/awesome-esp32-security/network/members)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)
[![ESP32 Security](https://img.shields.io/badge/Topic-esp32--security-blueviolet)](https://github.com/topics/esp32-security)
[![IoT Pentesting](https://img.shields.io/badge/Topic-iot--pentesting-orange)](https://github.com/topics/iot-pentesting)

> A hand-picked collection of ESP32 security tools, firmware analysis pipelines, IoT pentesting frameworks, and embedded hardware research resources.

The ESP32 family dominates the IoT landscape — from smart home devices to industrial controllers. This list gathers the most useful open-source projects for auditing, probing, and hardening these chips across WiFi, Bluetooth Low Energy, RF, and firmware layers.

---

## Contents

- [Firmware Analysis](#firmware-analysis)
- [WiFi Security & Monitoring](#wifi-security--monitoring)
- [Bluetooth Low Energy (BLE)](#bluetooth-low-energy-ble)
- [Radio Frequency Research](#radio-frequency-research)
- [Hardware & Forensics](#hardware--forensics)
- [Development Boards & Kits](#development-boards--kits)
- [Libraries & Frameworks](#libraries--frameworks)
- [Tutorials & Learning](#tutorials--learning)
- [Contributing](#contributing)
- [License](#license)

---

## Firmware Analysis

Tools for extracting, parsing, reversing, and auditing ESP32 firmware images.

| Project | What it does | Link |
|---------|-------------|------|
| **esptool.py** | Espressif's official utility for flashing, dumping, and inspecting flash contents | [GitHub](https://github.com/espressif/esptool) |
| **binwalk** | Firmware image extractor — parses partitions, bootloaders, and filesystems | [GitHub](https://https://github.com/ReFirmLabs/binwalk) |
| **Ghidra** | NSA reverse engineering suite with Xtensa (ESP32 ISA) decompiler support | [GitHub](https://github.com/NationalSecurityAgency/ghidra) |
| **Radare2 / rizin** | Lightweight RE framework; supports ESP32 binary analysis | [GitHub](https://github.com/radareorg/radare2) |
| **EMBA** | Automated firmware security analyzer with vulnerability detection | [GitHub](https://github.com/e-m-b-a/emba) |
| **Firmwalker** | Bash script that crawls extracted firmware for secrets, certs, keys | [GitHub](https://github.com/craigz28/firmwalker) |
| **FACT** | Firmware Analysis and Comparison Tool — web-based triage platform | [GitHub](https://github.com/fkie-cad/FACT_core) |
| **Firmware-Mod-Kit** | Extract, modify, and repackage firmware images | [GitHub](https://https://github.com/rampageX/firmware-mod-kit) |
| **Svace** | Static analysis tool with ESP-IDF project support | [Website](https://svace.ispras.ru/) |

---

## WiFi Security & Monitoring

Packet sniffing, deauth detection, rogue AP frameworks, and network reconnaissance using ESP32 hardware.

| Project | What it does | Link |
|---------|-------------|------|
| **ESP32 Marauder** | Feature-rich WiFi/BLE sniffer and attack firmware for ESP32 dev boards | [GitHub](https://github.com/justcallmekoko/ESP32Marauder) |
| **esp8266_deauther** | WiFi deauth, beacon spam, and probe flooding (ESP8266/ESP32) | [GitHub](https://github.com/SpacehuhnTech/esp8266_deauther) |
| **Evil Portal (Flipper)** | Captive portal phishing framework ported to ESP32 + Flipper Zero | [GitHub](https://github.com/bigbrodude6119/flipper-zero-evil-portal) |
| **Bettercap** | Network MITM and recon framework — pairs with ESP32 for wireless ops | [GitHub](https://github.com/bettercap/bettercap) |
| **Wireshark** | Industry-standard packet analyzer; handles pcap from ESP32 captures | [Website](https://www.wireshark.org/) |
| **WiFi-Pumpkin3** | Rogue access point framework for social engineering engagements | [GitHub](https://github.com/P0cL4bs/wifipumpkin3) |
| **Probe Request Scanner** | ESP32-based WiFi probe collector for device tracking research | [GitHub](https://github.com/schollz/ESP32-referencescan) |
| **Cowpatty** | WPA-PSK handshake cracker — works alongside ESP32 captures | [GitHub](https://github.com/joswr1ght/cowpatty) |

---

## Bluetooth Low Energy (BLE)

BLE sniffing, GATT exploitation, pairing attacks, and Bluetooth protocol analysis.

| Project | What it does | Link |
|---------|-------------|------|
| **Ubertooth One** | Open-source 2.4 GHz Bluetooth LE sniffer (works with ESP32 for TX) | [GitHub](https://github.com/greatscottgadgets/ubertooth) |
| **BtleJuice** | BLE MITM proxy — intercept and modify GATT transactions | [GitHub](https://github.com/DigitalIntelligence/btlejuice) |
| **nRF Sniffer** | Nordic's BLE sniffer for Wireshark — protocol-level capture | [GitHub](https://github.com/nordic-recipes/nrf-sniffer) |
| **gattacker** | BLE MITM framework for GATT service cloning and injection | [GitHub](https://github.com/AresS31/GATTacker) |
| **Sweyntooth** | Bluetooth vulnerabilities affecting BLE stacks (including ESP32) | [GitHub](https://github.com/Matheus-Garbelini/sweyntooth_bluetooth_low_energy_attacks) |
| **Braktooth** | ESP32-based Bluetooth Classic stack overflow exploit framework | [GitHub](https://github.com/Matheus-Garbelini/braktooth_esp32_bluetooth_classic_attacks) |
| **NimBLE** | Lightweight BLE stack for ESP32 — useful for building custom tools | [GitHub](https://github.com/apache/mynewt-nimble) |
| **BLE Spoofer** | ESP32 BLE advertisement spoofer for proximity and tracking tests | [GitHub](https://github.com/AresS31/esp32-ble-spoof) |

---

## Radio Frequency Research

Sub-GHz, LoRa, NFC, and wideband RF tools compatible with ESP32-based boards.

| Project | What it does | Link |
|---------|-------------|------|
| **Flipper Zero** | Multi-tool hardware platform — RF, NFC, iButton, Sub-GHz | [Website](https://flipperzero.one/) |
| **HackRF One** | Half-duplex SDR transceiver covering 1 MHz – 6 GHz | [GitHub](https://github.com/greatscottgadgets/hackrf) |
| **RTL-SDR** | Low-cost software defined radio receiver — ESP32 compatible via SPI | [Website](https://www.rtl-sdr.com/) |
| **LoRa ESP32** | Long-range low-power radio library for ESP32 | [GitHub](https://github.com/sandeepmistry/arduino-LoRa) |
| **rfcat** | RF analysis framework for Sub-GHz research | [GitHub](https://github.com/atlas0fd00m/rfcat) |
| **YARD Stick One** | Sub-1 GHz wireless transceiver for RF security work | [Website](https://greatscottgadgets.com/yardstick-one/) |
| **ESP32-RFID** | MFRC522 and PN532 RFID reader library for ESP32 | [GitHub](https://github.com/miguelbalboa/rfid) |
| **URH** | Universal Radio Hacker — analyze unknown IoT RF protocols | [GitHub](https://github.com/jopohl/urh) |

---

## Hardware & Forensics

Physical security, chip-off analysis, JTAG/SWD debugging, and memory extraction techniques.

| Project | What it does | Link |
|---------|-------------|------|
| **Bus Pirate** | Hardware hacking multi-tool — SPI, I2C, UART, JTAG | [GitHub](https://github.com/DangerousPrototypes/Bus_Pirate) |
| **Logic Analyzer (sigrok)** | Protocol analysis via Saleae-compatible logic analyzers | [Website](https://www.sigrok.org/) |
| **OpenOCD** | On-chip debugger for JTAG/SWD — direct ESP32 memory access | [GitHub](https://github.com/openocd-org/openocd) |
| **flashrom** | Chip reading/writing tool — dump ESP32 SPI flash directly | [Website](https://flashrom.org/) |
| **ChipWhisperer** | Side-channel analysis and glitching platform | [GitHub](https://github.com/newaetech/chipwhisperer) |
| **esptool.py flasher** | Read/write ESP32 flash partitions over UART | [GitHub](https://github.com/espressif/esptool) |
| **JTAGulator** | Auto-detect JTAG/UART pins on unknown boards | [GitHub](https://github.com/grandideast/JTAGulator) |
| **Tiger** | ESP32 memory forensics tool for RAM dump analysis | [GitHub](https://github.com/maciasr/esp32-dram-dump) |

---

## Development Boards & Kits

Recommended ESP32 hardware for security research and tool deployment.

| Board | Description | Buy |
|-------|-------------|-----|
| **ESP32-DevKitC** | Standard development board — most firmware tools target this | [Espressif](https://www.espressif.com/en/products/devkits/esp32-devkitc) |
| **ESP32-S3-DevKitC** | Newer variant with AI accelerator and USB OTG | [Espressif](https://www.espressif.com/en/products/devkits/esp32-s3-devkitc) |
| **ESP32-WROVER-IE** | Industrial-grade module with PSRAM for memory-intensive tools | [Espressif](https://www.espressif.com/en/products/modules/esp32-wrover) |
| **M5Stack Core2** | ESP32-based portable hacking kit with screen and battery | [M5Stack](https://m5stack.com/) |
| **TTGO T-Beam** | ESP32 + GPS + LoRa — ideal for mobile RF and tracker research | [GitHub](https://github.com/LilyGO/TTGO-T-Beam) |
| **Flipper Zero** | Not ESP32, but essential companion for RF/NFC/iButton work | [Flipper](https://flipperzero.one/) |
| **HackRF + PortaPack** | Standalone SDR hacking platform — complements ESP32 WiFi work | [GitHub](https://github.com/portapack-mayhem/mayhem-firmware) |

---

## Libraries & Frameworks

Core libraries and frameworks for building custom ESP32 security tools.

| Project | What it does | Link |
|---------|-------------|------|
| **ESP-IDF** | Espressif's official IoT Development Framework | [GitHub](https://github.com/espressif/esp-idf) |
| **Arduino ESP32** | Arduino core for ESP32 — rapid prototyping of security tools | [GitHub](https://github.com/espressif/arduino-esp32) |
| **PlatformIO** | Cross-platform build system with ESP32 toolchain support | [GitHub](https://github.com/platformio/platformio-core) |
| **MicroPython** | Python interpreter for ESP32 — scriptable security tools | [GitHub](https://github.com/micropython/micropython) |
| **CircuitPython** | Adafruit's Python fork with BLE and WiFi support | [GitHub](https://github.com/adafruit/circuitpython) |
| **ESPAsyncWebServer** | Async HTTP server for captive portal and phishing frameworks | [GitHub](https://github.com/me-no-dev/ESPAsyncWebServer) |
| **pcapng-parser** | Parse PCAP files captured by ESP32 WiFi monitor mode | [GitHub](https://github.com/simonwep/pcapng-parser) |
| **libesp32** | Low-level ESP32 C library for bare-metal security research | [GitHub](https://github.com/espressif/esp-idf) |

---

## Tutorials & Learning

Guides, courses, and walkthroughs for ESP32 security research.

| Resource | Description | Link |
|----------|-------------|------|
| **OWASP IoT Testing Guide** | Industry-standard IoT penetration testing methodology | [OWASP](https://owasp.org/www-project-internet-of-things/) |
| **Hacking the ESP32 Book** | Practical guide to ESP32 security and hardware hacking | [Amazon](https://www.amazon.com/dp/B09J7W8ZJ4) |
| **IoT Pentesting with ESP32** | Conference talks and workshop recordings on YouTube | [YouTube](https://www.youtube.com/results?search_query=esp32+pentesting) |
| **Marauder Wiki** | Comprehensive guide to using ESP32 Marauder firmware | [GitHub Wiki](https://github.com/justcallmekoko/ESP32Marauder/wiki) |
| **Exploiting IoT Devices (BSides)** | Conference presentation on ESP32 attack surfaces | [Slides](https://www.securitybsides.com/) |
| **ESP32 Security Whitepaper** | Espressif's official security architecture documentation | [Espressif](https://www.espressif.com/en/support/documents/technical-documents) |
| **Firmware Analysis Workshop** | Step-by-step firmware reversing walkthrough using ESP32 examples | [GitHub](https://github.com/Practical-IoT-Security/esp32-firmware-workshop) |
| **HackTricks IoT** | Quick reference for IoT and embedded device exploitation | [HackTricks](https://book.hacktricks.xyz/network-services-pentesting/iot-pentesting) |

---

## Contributing

Contributions welcome! Please read the [contribution guidelines](CONTRIBUTING.md) first. For new tool suggestions, open an issue or submit a pull request.

---

## License

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

<p align="center">
  <sub>Maintained by <a href="https://github.com/ykrishhh">ykrishhh</a> — Security Researcher & Developer</sub>
</p>
