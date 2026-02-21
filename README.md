# Group - 9

# Dual-Mode-Smart-Door-Lock-Fingerprint-RFID-project-phase--2  

# Dual‑Mode Smart Door Lock (Fingerprint + RFID) — ESP32  

---

# **IMPORTANT — WE ALSO BUILT A FULL PROTOTYPE IN TINKERCAD**  
###  **TinkerCAD Simulation (Fingerprint + RFID Door Lock Prototype):**  
### 🔗 https://www.tinkercad.com/things/8yYgeJT8fvm-copy-of-fingerprint-doorlock  
This prototype shows the **virtual circuit**, **RFID**, **fingerprint module**, **servo lock**, and **logic wiring**.  
We created this to demonstrate the concept visually before real‑hardware testing.  
**(Instructor‑friendly + visually clear + easy to demo!)**

---

> **Phase‑2 friendly:** This repo includes a **hardware‑free STUB build** you can compile and demo **without any sensors**, plus a **real‑hardware environment** using the same OOP codebase.

---

# 🛈 INFORMATION

- **No hardware today?**  
  Build the **stub environment**. It shows the local **SUCCESS** banner and GitHub Actions **green check**.  
  (Perfect for Phase‑2 demonstration.)

- **Have an ESP32 (but no sensors)?**  
  Upload the **stub firmware** and simulate everything from the **Serial Monitor** using your keyboard.

- **Have full hardware later?**  
  Switch to the **real environment** and wire RC522 + R307/AS608 + Relay as defined in `include/Config.h`.

---

#  Features

- **Dual authentication strategies (OOP):**  
  `RFIDAccess` and `FingerprintAccess` implement the common `AccessMethod` interface (Strategy Pattern).

- **EventBus (Observer Pattern):**  
  Publishes:  
  - `AccessGranted`  
  - `AccessDenied`  
  - `Locked`  
  - `Unlocked`  
  And is consumed by: `BuzzerLEDFeedback`.

- **Lock Actuator Abstraction:**  
  `LockActuator` → `SolenoidLockActuator` (relay/solenoid).  
  Includes **auto‑lock timer**.

- **Persistent Authorization:**  
  `AuthStorage` (LittleFS + ArduinoJson v7) stores `/authorized.json` containing:
  - `rfid_uids`
  - `fp_ids`

- **Admin Mode:**  
  Add/remove:
  - **RFID UIDs**
  - **Fingerprint template IDs**

  In STUB mode → controlled by **keyboard**  
  In REAL mode → controlled by **admin card + physical buttons**

---

# Most Important Environments

The **default environment** is the **stub** (no hardware required):

```ini
[platformio]
default_envs = esp32dev_stub

[env:esp32dev_stub]  # ✅ Build me for Phase‑2
platform = espressif32
board = esp32dev
build_flags = -D STUB_MODE=1
lib_deps = ArduinoJson @ ^7.0.4

[env:esp32dev_real]  # For later (real RC522 + R307 hardware)
platform = espressif32
board = esp32dev
lib_deps =
  ArduinoJson @ ^7.0.4
  miguelbalboa/MFRC522 @ ^1.4.10
  adafruit/Adafruit Fingerprint Sensor Library @ ^2.1.1
```
