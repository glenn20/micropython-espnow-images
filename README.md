# Precompiled Micropython ESPNow Images for the ESP32 and ESP8266
A collection of pre-compiled micropython images (including espnow support) for the esp32 and esp8266.

These are provided as a convenience for users until the ESPNow code is accepted into a Micropython release.

These images are compiled from the **espnow-g20*** branches at https://github.com/glenn20/micropython.

The Pull Request for ESPNow support is available at: https://github.com/micropython/micropython/pull/6515.

Documentation for the ESPNow module can be browsed at: https://micropython-glenn20.readthedocs.io/en/latest/library/espnow.html.

General micropython documentation at: https://docs.micropython.org/en/latest/reference/index.html.

Each folder contains the following firmware images:
- `firmware-esp32-GENERIC.bin`: For the ESP32 GENERIC build target.
- `firmware-esp8266-GENERIC_1M.bin`: For the ESP8266 GENERIC_1M build target (1MB RAM devices)
- `firmware-esp8266-GENERIC.bin`: For the ESP8266 GENERIC build target (2+MB RAM devices)


These images are built following the instructions at https://github.com/micropython/micropython/blob/master/ports/esp32/README.md and https://github.com/micropython/micropython/blob/master/ports/esp8266/README.md.

Images can be written to the ESP32 and ESP8266 devices over usb using esptool.py (install using pip), eg:

```
esptool.py --port /dev/ttyUSB0 --baud 115200 write_flash --flash_size=4MB --flash_mode=qio 0 firmware-esp8266-GENERIC_1M.bin
```

or

```
esptool.py --chip esp32 --port /dev/ttyUSB0 --baud 460800 write_flash -z 0x1000 firmware-esp32-GENERIC.bin
```

Firmware images are provided in the following folders:
- [20210128_espnow-g20_gba813d8f9](20210128_espnow-g20_gba813d8f9):
  - Branch **espnow-g20** (commit ba813d8f9) espnow patches applied against Micropython **master** on 28 Jan 2021.
- [20210128_espnow-g20-v113_gb560287eb](20210128_espnow-g20-v113_gb560287eb):
  - Branch **espnow-g20-v113** (commit b560287eb) espnow patches applied against Micropython release **v1.13** on 28 Jan 2021.
- [20210205_espnow-g20_g78be5dd0a](20210205_espnow-g20_g78be5dd0a):
  - Branch **espnow-g20** (commit 78be5dd0a) espnow patches applied against Micropython **master** on 5 Feb 2021.
- [20210205_espnow-g20-v114_g25840a12a](20210205_espnow-g20-v114_g25840a12a):
  - Branch **espnow-g20-v114** (commit 25840a12a) espnow patches applied against Micropython release **v1.14** on 5 Feb 2021.
- [20210415_espnow-g20_ga9bbf7083](20210415_espnow-g20_ga9bbf7083):
  - Branch **espnow-g20** espnow patches applied against Micropython **master** on 15 April 2021. Updated for fixes in broadcast message handling.
- [20210419_espnow-g20_v115_g020d5b1d1](20210419_espnow-g20_v115_g020d5b1d1):
  - Branch **espnow-g20** espnow patches applied against Micropython release **v1.15** on 19 April 2021. Updated for fixes in broadcast message handling.
- [20210511_espnow-g20_g2bb26c0a4](20210511_espnow-g20_g2bb26c0a4):
  - Branch **espnow-g20** espnow patches applied against Micropython main branch on 11 May 2021. Updated for fixes in co-existence with wifi and API change for recv()/irecv(). (Build against ESP IDF v4.2.1)
- [20210511_espnow-g20_v115](20210511_espnow-g20_v115):
  - Branch **espnow-g20** espnow patches applied against Micropython release **v1.15** on 19 April 2021. Updated for fixes in co-existence with wifi and API change for recv()/irecv(). (Build against ESP IDF v4.2.1)
- [20210812_espnow-g20_v116](20210812_espnow-g20-v116):
  - Branch **[espnow-g20-v116](https://github.com/glenn20/micropython/tree/espnow-g20-v116)** espnow patches applied against Micropython release **v1.16** on 12 August 2021.
- [20210903_espnow-g20-v1.17](20210903_espnow-g20-v1.17):
  - Branch **[espnow-g20-v1.17](https://github.com/glenn20/micropython/tree/espnow-g20-v1.17)** patches applied against Micropython release **v1.17** on 03 September 2021.
- [20211020_espnow-g20-v1.17-g26f058583](20211020_espnow-g20-v1.17-g26f058583): **ESP8266 Only** (Fix for [Issue #7](https://github.com/glenn20/micropython-espnow-images/issues/7))
  - Branch **[espnow-g20-v1.17](https://github.com/glenn20/micropython/tree/espnow-g20-v1.17)** patches applied against Micropython release **v1.17** on 20 October 2021.
