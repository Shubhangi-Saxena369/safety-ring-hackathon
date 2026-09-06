# safety-ring-hackathon
# Safety Ring — Automated Distress Detection Wearable

A smart ring concept that detects physical distress automatically, without requiring the wearer to press a button, and escalates through a phased alert protocol to family and police.

## The problem

Existing safety wearables (panic-button pendants, bracelets) rely on the victim manually triggering an alert. During a real assault, a victim may be restrained, frozen, or physically unable to press a button — making manual-only systems unreliable exactly when they're needed most.

## The approach

A dual-trigger system:

1. **Manual mode** — a tap pattern on the ring, for when a threat is sensed before an attack (e.g. being followed).
2. **AI mode (automated)** — passive detection using sensor fusion, for when the wearer is ambushed and cannot act.

### Sensors used (in the full hardware design)

| Signal | Sensor | What it detects |
|---|---|---|
| Skin sweat response | Galvanic Skin Response (GSR) | Sudden fear — sharp spike in skin conductance |
| Heart rate | Photoplethysmography (PPG) | Abnormal, rapid heart rate acceleration |
| Physical movement | 3D accelerometer + gyroscope | Chaotic, jerky motion vs. normal activity |
| Tamper detection | Continuous circuit loop | Ring being forcibly removed or destroyed |

Combining all three biometric signals (sensor fusion) avoids false alarms from ordinary activity like running to catch a train.

### Escalation protocol

- **0s** — Alert detected → audio/video recording starts, GPS locks
- **5s** — Family/emergency contacts notified with live location
- **10s** — Direct alert dispatched to police (ERSS-112), unless cancelled

Tamper detection (ring forcibly removed) skips straight to maximum alert.

## What's in this repo

- `sketch.ino` — ESP32 firmware (Wokwi simulation) implementing manual + motion-based trigger detection and the phased escalation logic
- `diagram.json` — Wokwi wiring diagram (push button + MPU6050 accelerometer)
- `safety-ring-demo.html` — interactive frontend mockup showing which sensors activate under different scenarios (walking normally, sensing a threat, being ambushed, ring tampering)

## Running the simulation

1. Open [Wokwi](https://wokwi.com), create a new ESP32 project
2. Paste `diagram.json` into the diagram tab and `sketch.ino` into the code tab
3. Add the `MPU6050` library via the Library Manager
4. Press Play — trigger the button or shake the virtual accelerometer to simulate a struggle

## Viewing the demo

Open `safety-ring-demo.html` directly in a browser, or visit the live GitHub Pages link for this repo.

## Note on scope

The frontend demo (`safety-ring-demo.html`) is a visual mockup of the intended user experience — it does not run live sensor logic. The Wokwi simulation is what proves the actual detection and escalation logic works.
