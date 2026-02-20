Group - 9

# Dual-Mode-Smart-Door-Lock-Fingerprint-RFID-project-phase--2

# Dual‑Mode Smart Door Lock (Fingerprint + RFID)  (ESP32)

> **Phase‑2 friendly:** this repo includes a **hardware‑free STUB build** you can compile and demo **without any devices**. It also ships a ready **real‑hardware** env for later, using the **same OOP architecture**.

---

## 🧭 TL;DR
- **No hardware today?** Build the **stub** env. Show the local **SUCCESS** banner and the **GitHub Actions green check**. For expected console output
- **Have an ESP32 (no sensors)?** Upload the **stub** firmware and simulate everything from the Serial Monitor using your keyboard.
- **Have full hardware later?** Switch to the **real** env and wire RC522 + R307/AS608 + relay as per `include/Config.h`.

---

## ✨ Features
- **Dual authentication strategies (OOP):** `RFIDAccess` and `FingerprintAccess` implement the `AccessMethod` interface (Strategy pattern).
- **EventBus (Observer):** publishes `AccessGranted/Denied`, `Locked/Unlocked`, consumed by `BuzzerLEDFeedback`.
- **Lock actuator abstraction:** `LockActuator` + `SolenoidLockActuator` (relay/solenoid). Auto‑lock timer built in.
- **Persistent authorization:** `AuthStorage` (LittleFS + ArduinoJson v7) stores `/authorized.json` with `rfid_uids` and `fp_ids`.
- **Admin Mode:** add/remove **RFID UIDs** and **FP template IDs** (in STUB, driven by keyboard; in real hardware, guarded by admin card + buttons).

---

## 🧱 Environments
The default env is the **stub** (no hardware).

```ini
[platformio]
default_envs = esp32dev_stub

[env:esp32dev_stub]  # ✅ build me for Phase‑2
platform = espressif32
board = esp32dev
build_flags = -D STUB_MODE=1
lib_deps = ArduinoJson @ ^7.0.4

[env:esp32dev_real]  # for later (real RC522 + R307)
platform = espressif32
board = esp32dev
lib_deps =
  ArduinoJson @ ^7.0.4
  miguelbalboa/MFRC522 @ ^1.4.10
  adafruit/Adafruit Fingerprint Sensor Library @ ^2.1.1
