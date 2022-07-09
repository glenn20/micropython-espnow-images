# Precompiled Micropython ESPNow Images for the ESP32 and ESP8266

A collection of pre-compiled micropython images (including espnow support) for
the esp32 and esp8266.

These are provided as a convenience for users until the ESPNow code is
accepted into a Micropython release.

These images are compiled from the **espnow-g20*** branches at
<https://github.com/glenn20/micropython>.

The Pull Request for ESPNow support is available at:
<https://github.com/micropython/micropython/pull/6515>.

Documentation for the ESPNow module can be browsed at:
<https://micropython-glenn20.readthedocs.io/en/latest/library/espnow.html>.

General micropython documentation at:
<https://docs.micropython.org/en/latest/reference/index.html>.

Each folder contains the following firmware images:

- `firmware-esp32-GENERIC.bin`: For the ESP32 GENERIC build target.
- `firmware-esp8266-GENERIC_1M.bin`: For the ESP8266 GENERIC_1M build target
  (1MB RAM devices)
- `firmware-esp8266-GENERIC.bin`: For the ESP8266 GENERIC build target (2+MB
  RAM devices)

These images are built following the instructions at
<https://github.com/micropython/micropython/blob/master/ports/esp32/README.md>
and
<https://github.com/micropython/micropython/blob/master/ports/esp8266/README.md>.

Images can be written to the ESP32 and ESP8266 devices over usb using
esptool.py (install using pip), eg:

```bash
esptool.py --port /dev/ttyUSB0 --baud 115200 write_flash --flash_size=4MB --flash_mode=qio 0 firmware-esp8266-GENERIC_1M.bin
```

or

```bash
esptool.py --chip esp32 --port /dev/ttyUSB0 --baud 460800 write_flash -z 0x1000 firmware-esp32-GENERIC.bin
```

or

```bash
esptool.py --chip esp32s2 --port /dev/ttyACM0 write_flash -z 0x1000 firmware-esp32-GENERIC_S2.bin
```

Firmware images are provided in the following folders:

- [20220709_espnow-g20-v1.19.1-espnow-6-g44f65965b](20220709_espnow-g20-v1.19.1-espnow-6-g44f65965b):
  - Branch
    **[v1.19.1-espnow-6-g44f65965b](https://github.com/glenn20/micropython/tree/v1.19.1-espnow-6-g44f65965b)**
    patches applied against Micropython release **v1.19.1**.
    - Fixup for callback methods: **ESPNow.irq()** and **ESPNow.on_recv()**:
      - See docs at:
        <https://micropython-glenn20.readthedocs.io/en/latest/library/espnow.html#callback-methods>.
      - New tests in tools/multi_espnow/15_irq_test.py.

- [20220706_espnow-g20-v1.19.1-espnow-4-g537248958](20220706_espnow-g20-v1.19.1-espnow-4-g537248958):
  - Branch
    **[v1.19.1-espnow-4-g537248958](https://github.com/glenn20/micropython/tree/espnow-g20-v1.19.1)**
    patches applied against Micropython release **v1.19.1**.
    - Built on latest espnow-g20 patches rebased against v1.19.1 micropython
      release tag.
    - **API Change**:
      - Use `import espnow` instead of `from esp import espnow`.
        - This is necessitated by the recent simplification of the C module
          supported by a python wrapper module: [espnow.py](https://github.com/glenn20/micropython/blob/espnow-g20/ports/esp32/modules/espnow.py).
      - `.recv()` and `.any()` method supported on esp8266
      - `.any()` method and iterator support on esp8266
      - asyncio support on esp8266 (for GENERIC target - ie. devices with >= 2MB
        flash))
      - Add `.recvinto()` method for esp32 and esp8266
    - Updated docs at <https://micropython-glenn20.readthedocs.io/en/latest/library/espnow.html>.
- [20220423_espnow-g20-v1.18-14-g78cdcdfdc](20220423_espnow-g20-v1.18-14-g78cdcdfdc):
  - Branch
    **[espnow-g20-v1.18](https://github.com/glenn20/micropython/tree/espnow-g20-v1.18)**
    patches applied against Micropython release **v1.18** on 23 April 2022.
    - Includes: RSSI monitoring, asyncio support (aioespnow.py)
      - New implementation of RSSI monitoring (no change to user API)
        - RSSI of first message(s) from peer is no longer lost
        - Device table is updated on call to recv()/irecv(), so you must read
          the message out of the buffers before the rssi value is updated in
          e.peers (see docs). This also reduces the workload in the internal
          function (espnow_recv_cb()).
    - ESP32 images are built with v4.2 IDF
      - If `micropython.mem_info()` was only showing ~64k RAM, this should be
        fixed
    - ESP32S2 and ESP32C3 are built with v4.4 IDF.
    - No new ESP8266 images as there are no differences from prior uploads.

- [20220413_espnow-g20-v1.18-10-ge68d28c8b](20220413_espnow-g20-v1.18-10-ge68d28c8b):
  - Branch **[espnow-g20-v1.18](https://github.com/glenn20/micropython/tree/espnow-g20-v1.18)** patches applied against Micropython release v1.18 on 13 April 2022.
    - Includes:
      - RSSI monitoring support
      - New asyncio support (aioespnow.py)
        - (see
          https://micropython-glenn20.readthedocs.io/en/latest/library/espnow.html#supporting-asyncio-esp32-only)
      - Removed Buffer Protocol support (including read(), read1(), readinto(),
        write() methods)
- [20220408_espnow-g20-rssi-v1.18-6-g24cf16719](20220408_espnow-g20-rssi-v1.18-6-g24cf16719):
  - Branch **[espnow-g20-rssi-v1.18](https://github.com/glenn20/micropython/tree/espnow-g20-rssi-v1.18)** patches applied against Micropython release v1.18 on 08 April 2022.
    - Based on RSSI feature branch
      - Includes support for monitoring RSSI values of recieved messages.
    - Built against ESP IDF v4.4 (i2c support may be broken).
- [20220407_espnow-g20-v1.18-3-geaf7fd7d4](20220407_espnow-g20-v1.18-3-geaf7fd7d4):
  - Branch **[espnow-g20-v1.18](https://github.com/glenn20/micropython/tree/espnow-g20-v1.18)** patches applied against Micropython release v1.18 on 07 April 2022.
    - Includes builds for all of the new esp32 S2/S3/C3 targets.
      - I have tested GENERIC, UM_TINYS2, UM_FEATHERS2 and GENERIC_S2). The
        other images are untested.
    - Built against ESP IDF v4.4 (i2c support may be broken).
- [2021113_espnow-g20-v1.17-142-gbb9aac55a](2021113_espnow-g20-v1.17-142-gbb9aac55a):
  - Branch
    **[espnow-g20-dev](https://github.com/glenn20/micropython/tree/espnow-g20-dev)**
    applied against Micropython master (ff4f1f3a) on 13 November 2021.

    - Includes builds for all of the new esp32 S2/S3/C3 targets. Warning - most of these builds are untested.

- [20211111_espnow-g20-v1.17-142-g8e1fcd490](20211111_espnow-g20-v1.17-142-g8e1fcd490):
  - Branch
    **[espnow-g20-dev](https://github.com/glenn20/micropython/tree/espnow-g20-dev)**
    applied against Micropython master (ff4f1f3a) on 11 November 2021.

    - Includes latest buffer optimisations and support for on_recv on esp8266.
- [20211104_espnow-g20-v1.17_ESP32S2](20211104_espnow-g20-v1.17_ESP32S2):
  - Includes espnow-enabled firmware image for the ESP32S2 targets available
    in v1.17 (compiled with ESP IDF v4.3.1):
    - GENERIC_S2 (no SPIRAM support),
      [UM_TINYS2](https://unexpectedmaker.com/tinys2) and
      [UM_FEATHERS2](https://feathers2.io/)
      - The UM_* targets include support for the SPIRAM and some additional
        board support modules from UM:
        ([feathers2.py](https://github.com/micropython/micropython/blob/v1.17/ports/esp32/boards/UM_FEATHERS2/modules/feathers2.py)
        and
        [tinys2.py](https://github.com/micropython/micropython/blob/v1.17/ports/esp32/boards/UM_TINYS2/modules/tinys2.py)).
      - Unfortunately there is no generic S2 image available for v1.17 with
        SPIRAM support.
- [20211020_espnow-g20-v1.17-g26f058583](20211020_espnow-g20-v1.17-g26f058583):
  **ESP8266 Only** (Fix for [Issue
  #7](https://github.com/glenn20/micropython-espnow-images/issues/7))
  - Branch
    **[espnow-g20-v1.17](https://github.com/glenn20/micropython/tree/espnow-g20-v1.17)**
    patches applied against Micropython release **v1.17** on 20 October 2021.
- [20210903_espnow-g20-v1.17](20210903_espnow-g20-v1.17):
  - Branch
    **[espnow-g20-v1.17](https://github.com/glenn20/micropython/tree/espnow-g20-v1.17)**
    patches applied against Micropython release **v1.17** on 03 September
    2021.
- [20210812_espnow-g20_v116](20210812_espnow-g20-v116):
  - Branch
    **[espnow-g20-v116](https://github.com/glenn20/micropython/tree/espnow-g20-v116)**
    espnow patches applied against Micropython release **v1.16** on 12 August
    2021.
- [20210511_espnow-g20_v115](20210511_espnow-g20_v115):
  - Branch **espnow-g20** espnow patches applied against Micropython release
    **v1.15** on 19 April 2021. Updated for fixes in co-existence with wifi
    and API change for recv()/irecv(). (Build against ESP IDF v4.2.1)
- [20210511_espnow-g20_g2bb26c0a4](20210511_espnow-g20_g2bb26c0a4):
  - Branch **espnow-g20** espnow patches applied against Micropython main
    branch on 11 May 2021. Updated for fixes in co-existence with wifi and API
    change for recv()/irecv(). (Build against ESP IDF v4.2.1)
- [20210419_espnow-g20_v115_g020d5b1d1](20210419_espnow-g20_v115_g020d5b1d1):
  - Branch **espnow-g20** espnow patches applied against Micropython release
    **v1.15** on 19 April 2021. Updated for fixes in broadcast message
    handling.
- [20210415_espnow-g20_ga9bbf7083](20210415_espnow-g20_ga9bbf7083):
  - Branch **espnow-g20** espnow patches applied against Micropython
    **master** on 15 April 2021. Updated for fixes in broadcast message
    handling.
- [20210205_espnow-g20-v114_g25840a12a](20210205_espnow-g20-v114_g25840a12a):
  - Branch **espnow-g20-v114** (commit 25840a12a) espnow patches applied
    against Micropython release **v1.14** on 5 Feb 2021.
- [20210205_espnow-g20_g78be5dd0a](20210205_espnow-g20_g78be5dd0a):
  - Branch **espnow-g20** (commit 78be5dd0a) espnow patches applied against
    Micropython **master** on 5 Feb 2021.
- [20210128_espnow-g20-v113_gb560287eb](20210128_espnow-g20-v113_gb560287eb):
  - Branch **espnow-g20-v113** (commit b560287eb) espnow patches applied
    against Micropython release **v1.13** on 28 Jan 2021.
- [20210128_espnow-g20_gba813d8f9](20210128_espnow-g20_gba813d8f9):
  - Branch **espnow-g20** (commit ba813d8f9) espnow patches applied against
    Micropython **master** on 28 Jan 2021.
