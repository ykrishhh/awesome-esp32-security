<div align="center">

<img src="assets/logo.svg" width="400" alt="Awesome ESP32 Security">

# Awesome ESP32 Security

> Curated ESP32 security tools, firmware, and resources for pentesters and IoT researchers.

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](LICENSE)
[![Stars](https://img.shields.io/github/stars/ykrishhh/awesome-esp32-security?style=for-the-badge&color=green)](https://github.com/ykrishhh/awesome-esp32-security)

</div>

---

## Features

| Category | Tools |
|----------|-------|
| Firmware Analysis | esptool.py, Binwalk, FACT |
| WiFi/BLE Attacks | WiFi Deauther, Bluetooth Explorer |
| Hardware Hacking | JTAG/UART, Bus Pirate, Logic Analyzers |
| Tools & Frameworks | ESP-IDF, PlatformIO, Micropython |

## Quick Start

```bash
git clone https://github.com/ykrishhh/awesome-esp32-security.git
cd awesome-esp32-security
```

## ESP32 Hardware Security Architecture

To secure an ESP32 deployment against both remote and physical attack vectors, the hardware architecture relies on a series of cryptographic and isolation mechanisms built into the silicon. Below is a structured threat-model mapping of ESP32's built-in security controls:

```mermaid
graph TD
    subgraph Attacks["Threat & Attack Vectors"]
        A1["Physical Flash Dumping (SPI Sniffing)"]
        A2["Glitching & Side-Channel (Voltage/Clock)"]
        A3["Malicious Firmware Flash (Remote/Physical)"]
        A4["JTAG/OCD Hardware Debug Probe Access"]
    end

    subgraph HardwareControls["ESP32 Core Cryptographic Controls"]
        C1["Flash Encryption (AES-256)"]
        C2["Secure Boot (V1/V2 Cryptographic Signatures)"]
        C3["Hardware JTAG Disable (eFuse LOCK)"]
        C4["Silicon eFuses (One-Time Programmable)"]
    end

    subgraph DefenseState["Secured Target State"]
        S1["Confidential Firmware & Keys"]
        S2["Immutable Trust Anchor (ROM Bootloader)"]
        S3["Locked Debug Port (Anti-Reversing)"]
        S4["Untamperable Hardware Config"]
    end

    A1 -->|Blocked by| C1
    A3 -->|Blocked by| C2
    A4 -->|Blocked by| C3
    A2 -->|Mitigated by| C4

    C1 -->|Ensures| S1
    C2 -->|Ensures| S2
    C3 -->|Ensures| S3
    C4 -->|Protects| S4
    
    style Attacks fill:#1a0f0f,stroke:#7a1a1a,stroke-width:2px,color:#fff
    style HardwareControls fill:#0f1a0f,stroke:#1a7a1a,stroke-width:2px,color:#fff
    style DefenseState fill:#0f141a,stroke:#1a4d7a,stroke-width:2px,color:#fff
```

## BLE Security Tools

| Tool | Description | Platform |
|------|-------------|----------|
| [nRF Connect](https://play.google.com/store/apps/details?id=no.nordicsemi.android.mcp) | BLE scanner and debugger | Android/iOS |
| [BLE Scanner](https://play.google.com/store/apps/details?id=com.macdom.ble.blescanner) | Scan and explore BLE devices | Android |
| [GATTacker](https://github.com/AresS31/GATTacker) | BLE man-in-the-middle framework | Linux |
| [Bettercap](https://www.bettercap.org/) | BLE sniffing and attacks | Cross-platform |
| [Sweyntooth](https://asset-group.github.io/disclosures/sweyntooth/) | BLE vulnerabilities exploitation | Research |
| [Braktooth](https://github.com/Matheus-Garbelini/braktooth_esp32_bluetooth_classic_attacks) | ESP32 BT Classic attacks | ESP32 |

## Troubleshooting

Hit a wall with SPI/I2C, NRF24L01, power, flashing, or serial? See the
[ESP32 Security Troubleshooting Guide](docs/troubleshooting.md) — real fixes for
the failures that eat your first day.

## Contributing

Contributions welcome!

## License

[MIT License](LICENSE) — Built by [ykrishhh](https://github.com/ykrishhh)

---

<div align="center">

**Star this repo if you find it useful!** ⭐

</div>
