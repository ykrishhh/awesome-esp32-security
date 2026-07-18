# ESP32 Security Project Troubleshooting Guide

A field guide for ESP32 security researchers. Covers the failures that eat your
first day: buses that won't initialize, radios that won't talk, brownouts, and
firmware that won't flash. Each section has the symptom, the likely cause, and a
fix that works on real hardware — not just in the datasheet.

---

## 1. SPI / I2C Initialization Failures

**Symptom:** `begin()` returns `false`, sensor reads `0xFF` / `0x00`, or the
bus hangs on the first transaction.

| Cause | Fix |
|-------|-----|
| Wrong SDA/SCL or MOSI/MISO pin for the board variant | ESP32 has remappable peripherals — pass explicit pins: `Wire.begin(SDA, SCL)` for I2C, `SPI.begin(SCK, MISO, MOSI, CS)` for SPI. Don't assume the dev-board silkscreen. |
| Two I2C devices share an address | Scan the bus: `i2c_detect` / `i2cdetect -y 1` (Linux) or run an `Wire` scanner sketch. Use an address shifter or a TCA9548A mux. |
| SPI CS left floating / not driven | Drive CS manually for shared buses, or assign a dedicated GPIO per device. A floating CS causes intermittent `0xFF` frames. |
| 3.3 V vs 5 V logic mismatch | Most ESP32 pins are **not 5 V tolerant**. Level-shift I2C (bidirectional) and SPI (unidirectional) before connecting 5 V sensors. |
| Incorrect pull-up on I2C | I2C needs 4.7 kΩ pull-ups to 3.3 V on SDA + SCL. On-board modules often omit them — add your own. |

> Debugging trick: slow the bus first. `Wire.setClock(50000)` (I2C) or
> `SPI.setFrequency(100000)` rules out timing/glitch issues before you chase
> wiring.

---

## 2. NRF24L01 Connection Issues

**Symptom:** `radio.printDetails()` shows all `0x00` or `0xFF`, `radio.isChipConnected()`
is `false`, or packets never arrive.

| Cause | Fix |
|-------|-----|
| **Under-voltage** — NRF24L01 spikes to ~20–30 mA on TX and brownouts the ESP32 3.3 V rail | Power the module from a **dedicated 3.3 V LDO** (e.g. AMS1117), not the ESP32's onboard regulator. Add a 10 µF cap at the module VCC. This is the #1 cause of "it worked for a second then died." |
| Missing 100 nF **decoupling cap** at the module | Solder a 0.1 µF ceramic directly across VCC/GND on the module. Without it, RF noise corrupts the SPI bus. |
| SPI pins not wired to the ESP32's VSPI/HSPI | Default RF24 Arduino lib uses fixed SPI pins — match them or pass `SPIClass` explicitly. Mismatched MISO/MOSI = silent failure. |
| CE/CSN on wrong GPIO | CSN is the SPI CS (active low); CE is the mode pin. Swapping them is the classic "chip not found." |
| 2.4 GHz congestion / auto-ACK timeout | Lower `setDataRate(RF24_1MBPS)`, `setChannel()` away from WiFi ch 1/6/11, and `setRetries(5, 15)`. |

> RF security note: NRF24 is unencrypted by default. For MITM / replay research,
> `radio.sniff` patterns and replay captured payloads — but keep it on your own
> hardware and isolated test gear.

---

## 3. Power Supply Problems

**Symptom:** Random resets, `Guru Meditation` / `InstrFetchProhibited`, WiFi
won't associate, or the chip reboots under load.

| Cause | Fix |
|-------|-----|
| Brownout on TX / flash write | Set `menuconfig → Component config → ESP32-specific → Minimum brownout threshold` to 2.7–2.9 V, **or** feed clean 3.3 V. The brownout detector firing under RF load is normal on weak supplies. |
| USB port can't supply peak current | ESP32 + radio can draw 300+ mA spikes. Use a powered hub or a 1 A+ supply, not a laptop's sleep-current port. |
| Noise coupling onto 3.3 V from DC-DC | Add bulk (10–100 µF) + decoupling (0.1 µF) caps at the module. Switch-mode supplies without caps reset the chip on every TX. |
| Wrong input voltage to board | Dev boards regulate **5 V in**. Feeding 3.3 V into the 5 V pin (or vice-versa) kills the regulator. Check the silkscreen. |

> Measure, don't guess: put a scope / DMM on the 3.3 V rail during a TX burst.
> If it dips below ~2.9 V, that's your bug.

---

## 4. Flash / Firmware Errors

**Symptom:** `esptool.py` fails with `Failed to connect`, `Timed out waiting
for packet header`, or `Invalid head of packet`.

| Cause | Fix |
|-------|-----|
| Not in download mode | Hold **BOOT**, tap **EN/RST**, release BOOT. Or wire AUTO-RTS/DTR so esptool toggles it. Some clones need manual entry every time. |
| Wrong COM port / permissions | `ls /dev/tty*` (Linux) / Device Manager (Win). On Linux add your user to `dialout`, or `sudo chmod 666 /dev/ttyUSB0` for a test. |
| Wrong baud rate | Lower to `esptool.py --baud 115200` (or 9600). High baud on a noisy cable droputs the handshake. |
| Stale / wrong esptool | `pip install -U esptool`. Mismatched esptool vs chip (ESP32-C3/S3 vs classic) throws CRC errors. |
| Flash size mismatch | Pass `--flash_size=4MB` (or your part). Wrong size bricks OTA partitions and breaks boot. |
| Protected eFuses / flash read-prot | If `esptool` reads `0x00`/`0xFF` everywhere and `flash_id` fails, the part may be read-locked — note it, don't keep hammering (risks bricking). |

Useful commands:
```bash
# identify the chip + flash
esptool.py flash_id
# read back firmware for analysis (if not protected)
esptool.py read_flash 0x00000 0x400000 fw.bin
# basic connectivity test
esptool.py chip_id
```

---

## 5. Serial Communication Debugging

**Symptom:** Garbage on the monitor, no output at all, or `Serial` prints but
you can't get a shell.

| Cause | Fix |
|-------|-----|
| Baud mismatch | ESP32 bootloader is **115200**; your app may use 9600/115200/921600. Match `idf.py monitor` / `miniterm.py` to the app. Garbage chars = baud is wrong. |
| Wrong UART selected | `Serial` = UART0 (often tied to the USB-serial chip). `Serial1`/`Serial2` need explicit TX/RX GPIOs. Don't print to a UART with no wires. |
| GPIO strapping pins pulled wrong at boot | Pins 0, 2, 5, 6–11, 12–15 have boot-time functions. A pulledLOW/HIGH on a strapping pin changes boot mode — that's why "it won't boot normally." |
| DTR/RTS toggling the wrong lines | Some adapters assert RTS to EN. If the chip won't stay in boot mode, disable `idf.py monitor` auto-reset or use `esptool` manual mode. |
| CRLF / line-ending mismatch | Use `\r\n` if your terminal expects it; monitor shows partial lines otherwise. |

> Hardware RE tip: a logic analyzer on the TX/RX lines during boot captures the
> early boot log even when the USB-serial chip is misbehaving — essential when
> you can't get a monitor session at all.

---

## Quick Diagnostic Order

1. **Power first.** Scope the 3.3 V rail under load. Most "weird" bugs are power.
2. **Baud + bus speed.** Drop both, confirm comms, then raise.
3. **Scan the bus / `flash_id`.** Confirm the chip is physically present.
4. **Watch the strap pins.** A wrong pull = wrong boot mode.
5. **Isolate RF.** Power NRF24 from its own LDO before blaming code.

---

*Built by [ykrishhh](https://github.com/ykrishhh) for the Awesome ESP32 Security list.*
