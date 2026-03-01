# Flashing compiled binaries

Flashing the ESP32-C3 Super Mini board via the web browser is only possible while having physical access to the "boot" button. The method via esptool.py will also work via the USB data line pass-through of the USB-C port on the housing.

## esptool.py

Use the following command to flash with `esptool.py` (included in ESP-IDF and Arduino-ESP32 core installations). Run from this directory or adjust paths. Change `COM1` to your port.

```bash
esptool.py -p COM1 -b 460800 --before default_reset --after hard_reset --chip esp32c3 write_flash --flash_mode dio --flash_freq 80m --flash_size detect 0x0 bootloader.bin 0x8000 partition-table.bin 0x10000 THERMAL_MONOCULAR.bin
```

## Web browser

1. Visit [esp.huhn.me](https://esp.huhn.me/) (Chrome recommended; other browsers may not work).

2. Hold down the **Boot** button, insert the USB cable, then release the button.

3. Click **Connect** and select the serial port of the ESP32 board.

4. Add the following files at the given flash offsets:
   - `bootloader.bin` → **0x0**
   - `partition-table.bin` → **0x8000**
   - `THERMAL_MONOCULAR.bin` → **0x10000**

5. Click **ERASE** and wait for the flash to be erased.

6. Click **PROGRAM**.
