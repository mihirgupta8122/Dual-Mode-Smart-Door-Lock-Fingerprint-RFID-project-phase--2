
# Dual‑Mode Smart Door Lock (Fingerprint + RFID) (ESP32)

**Runs without hardware (STUB mode)** and supports real sensors later.

## Environments
- **esp32dev_stub (default)** → no hardware required. Simulate RFID/FP/Admin via Serial.
- **esp32dev_real** → real modules (RC522 + R307/AS608 + relay) when hardware is available.

## Quick Demo (no hardware)
1. Open this folder in VS Code (PlatformIO installed).
2. Build: PlatformIO ✓ Build (or `pio run -e esp32dev_stub`).
3. (Without a board you can skip Serial Monitor.) To show expected output, see `docs/sample-serial-output.txt`.
4. Push to GitHub: CI at `.github/workflows/build.yml` compiles the stub env on each push.

## With an ESP32 (still no sensors)
1. Plug ESP32 via USB → Build → Upload → Monitor @ 115200.
2. In Serial Monitor type:
   - `r` → simulate RFID success (unlock)
   - `p` → simulate Fingerprint success (unlock)
   - `a` → Admin window (10s): `e` enroll ID, `d` delete ID, `c` authorize UID, `x` remove UID
3. Auto‑lock triggers after 5s by default.

## Storage
Authorization list lives at `/authorized.json` (LittleFS):
```json
{"rfid_uids":["DE AD BE EF"], "fp_ids":[1,7,12]}
```

## Notes
- STUB mode removes **sensor I/O**, but keeps the same OOP architecture.
- Later, switch to `esp32dev_real` and wire hardware per `include/Config.h`.
