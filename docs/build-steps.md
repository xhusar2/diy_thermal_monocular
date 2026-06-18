# Build Steps

## Prerequisites

All parts for assembly

- All parts from the [BOM](BOM.md)
- 3D printed body parts
- Soldering iron
- Hex/Allen key set
- Tweezers
- Hot glue gun (optional, for securing wires)

---

## Overview

Assembly has two parallel workstreams that come together at final body installation:

- **Board assembly** — ESP32 soldered to the potentiometer board and OLED display board per the [wiring diagram](../resources/wiring/)
- **Power subassembly** — DC power inlet and power button wired separately, with longer cable tails, because they must be soldered last after fitting into the body

---

## Step 1 — Body Preparation

- 1.1 Install heated inserts into the main body — 8× M2
- 1.2 Install heated insert for picatinny/RIS mount — 1× M5
- 1.3 Install heated insert for J-arm mount — 1× M6
- 1.4 Install the RIS rail adapter

---

## Step 2 — Pre-Soldering Preparation

### 2.1 Board subassembly

Remove unnecessary cables from the OLED display board accordging to the image
![Remove unnecessary cables](resources/build_photos/build_remove_cables.jpg)

Solder the ESP32-C3 Super Mini to the potentiometer board and the OLED display board according to the wiring diagram. Keep cable tails short on these connections.

### 2.2 Power subassembly

Solder the DC power inlet and power button as a separate subassembly. **Leave sufficient cable length** on these — they are inserted into the body later and soldered in place after fitting, so short cables will make final assembly impossible.

### 2.3 Buck converter wiring preparation

Prepare the buck converter by soldering the capacitors on the VIN/VOUT side.
![Solder buck converter](resources/build_photos/build_buck.jpg)

### 2.4 Ground cable preparation

Cut and prepare grey ground cables:

- 3× longer ground cables
- 2× shorter ground cables



### 2.5 5V cable preparation

Cut 5V power cables to **~4 cm** length.
![Prepare cables](resources/build_photos/build_cables_5v.jpg)

---

## Step 3 — Soldering

### 3.1 Buck converter ground

Solder ground cables to the buck converter output ground pad and to the ESP32 ground pin.
![Solder cables](resources/build_photos/build_esp_to_buck.jpg)


### 3.2 Ground bus

Solder all ground cables together onto the common ground bus.

### 3.3 5V bus

Solder all 5V cables onto the common 5V bus.

### 3.4 ESP32, buttons, and potentiometer

Solder signal wires to:

- ESP32 GPIO pins (per wiring diagram)
- All push buttons
- Potentiometer wiper and end pins

---

## Step 4 — Final Body Assembly

### 4.1 Power inlet and switch installation

1. Insert the DC power inlet into the body opening.
2. Insert the power button into its opening.
3. Once seated, **carefully solder** the ground wire from the buck converter and the 5V wire to the power switch terminals.
4. Use a short jumper wire to bridge the DC inlet to the switch to close the power circuit.

> Soldering order matters here — components must be physically in place first, then soldered.

### 4.2 Potentiometer and buttons

1. Insert the potentiometer through its opening and secure with the retaining nut.
2. Insert all push buttons through their openings and secure with retaining nuts.

### 4.3 Thermal camera sensor

Attach the thermal camera sensor and assemble the camera case around it.

### 4.4 Display and frame

Attach the OLED display to the front frame, then insert the frame assembly into the body. At this moment its useful to check if everything works by connecting to DC inlet. OLED shoud come on. Now before we secure sensor and display, we can check the orientation of the image so the sensor and display align. We can later flip the image verticaly if its needed (also horizontaly if necessary).  Secure with M3 screws.

---

## Step 5 — Final Testing

After everything is secured we test again. 

1. Connect 5V to the DC inlet.
2. Press the power button — the device should boot and the OLED should come on.
3. Cycle through all push buttons and verify each is recognized in the menu.
4. Turn the potentiometer through its full range and verify response.

---


### Flash pre-compiled binaries

See [compiled_binaries/README.md](../compiled_binaries/README.md) for flashing via `esptool.py` or the web flasher.

### Build from source (Windows — ESP-IDF PowerShell)

1. Open **ESP-IDF CMD** (installed with ESP-IDF — use the shortcut from the Start menu, not a plain PowerShell window, so the environment is pre-loaded).
2. Navigate to the source directory:
  ```powershell
   cd path\to\night_vision_devices-thermal_monocular\source_code
  ```
3. Set the target chip:
  ```powershell
   idf.py set-target esp32c3
  ```
4. Build:
  ```powershell
   idf.py build
  ```
5. Flash (replace `COM1` with your port):
  ```powershell
   idf.py -p COM1 flash
  ```
   Or use `esptool.py` directly with the binaries from `build/` — see [compiled_binaries/README.md](../compiled_binaries/README.md) for the exact offsets.

> The firmware was compiled with **esp-idf v5.5.3**. Other versions may require dependency adjustments.

---

## Finished Product


<TODO ADD PHOTOS>