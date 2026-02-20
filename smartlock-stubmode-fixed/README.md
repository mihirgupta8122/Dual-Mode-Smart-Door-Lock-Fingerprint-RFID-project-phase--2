# Dual‑Mode Smart Door Lock (Fingerprint + RFID) — ESP32 (Phase‑2)

This repository contains the **Phase‑2 firmware** for a dual‑authentication smart door‑lock system using **RFID + Fingerprint**.  
The design focuses on **software architecture, OOP principles, storage, and controller logic**, while the **hardware modules will be added in later phases**.

➡️ **IMPORTANT:**  
This version of the firmware runs in **STUB MODE**, meaning it **works only in a basic, terminal‑level simulation**.  
tjhere is no need  **do NOT need any hardware** to build or test this Phase‑2 version.  
However, to achieve **full real-world functionality**, you will need actual hardware in future phases (ESP32 board, RFID RC522, Fingerprint R307/AS608, relay/solenoid).

---

## 🌟 Features (Phase‑2)
- Full **Object‑Oriented Architecture**
  - `AccessMethod` interface (Strategy Pattern)
  - `RFIDAccess` & `FingerprintAccess` modules
  - `LockActuator` abstraction (`SolenoidLockActuator`)
  - `LockController` orchestrates OR‑logic and auto‑lock

- **EventBus (Observer Pattern)** for internal communication  
  Decouples authentication modules from feedback systems.

- **Persistent Storage**  
  `/authorized.json` saved using **LittleFS + ArduinoJson v7**  
  Stores:
  ```json
  {
    "rfid_uids": ["DE AD BE EF"],
    "fp_ids": [1, 7, 12]
  }
