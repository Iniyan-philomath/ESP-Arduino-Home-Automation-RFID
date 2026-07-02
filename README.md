# ESP Arduino Projects

A polished GitHub-ready repository containing two ESP-based Arduino systems with separate folders, clear documentation, wiring guides, and upload-ready sketches.

---

## 🚀 Projects Included

### 1. ESP8266 RFID Room Control
- **Folder:** `ESP8266-RFID-Room-Control/`
- **Sketch:** `ESP8266-RFID-Room-Control.ino`
- **Board:** ESP8266 NodeMCU
- **Purpose:** Secure room control using ESP-NOW authorization, automatic temperature/light sensing, and relay-driven fan/lamp control.

### 2. ESP32 Drowsiness Monitor
- **Folder:** `ESP32-Drowsiness-Monitor/`
- **Sketch:** `ESP32-Drowsiness-Monitor.ino`
- **Board:** ESP32
- **Purpose:** MQTT-based alert monitor that shows drowsiness warnings via LEDs.

---

## 📁 Repository Structure

- `README.md` — top-level project overview and setup instructions.
- `CONTRIBUTING.md` — contribution guidelines.
- `HARDWARE.md` — component list and wiring instructions.
- `.gitignore` — ignores Arduino and temporary files.
- `LICENSE` — MIT license.
- `ESP8266-RFID-Room-Control/` — ESP8266 project files.
- `ESP32-Drowsiness-Monitor/` — ESP32 project files.

---

## 📦 Components

### Shared Requirements
- USB power source or stable regulator
- Arduino IDE or PlatformIO
- ESP board support installed

### ESP8266 RFID Room Control
- ESP8266 NodeMCU
- DHT11 temperature and humidity sensor
- LDR light sensor
- 2-channel relay module
- RGB LED or 3 separate LEDs
- ESP-NOW sender device / card scanner

### ESP32 Drowsiness Monitor
- ESP32 development board
- Red LED
- Green LED
- 220Ω resistors

---

## 🧠 Architecture

### ESP8266 RFID Room Control
This sketch acts as an ESP-NOW receiver and automation controller:
- Waits for a valid authorization packet.
- Reads temperature/humidity from DHT11.
- Reads ambient light from the LDR.
- Activates fan relay when temperature is high.
- Activates lamp relay when ambient light is low.
- Uses RGB LED for status feedback.
- Shuts down outputs when authorization is lost.

### ESP32 Drowsiness Monitor
This sketch acts as an MQTT client:
- Connects to Wi-Fi.
- Connects to an MQTT broker.
- Subscribes to the `led/control` topic.
- Parses alert values and updates LEDs.
- Reconnects automatically if the connection drops.

---

## 🔄 Workflow

### ESP8266 RFID Room Control
1. Power on the ESP8266 NodeMCU.
2. Initialize ESP-NOW and wait for a remote authorization packet.
3. If `authorized == true`, enable sensors and automation.
4. Read DHT11 and LDR values periodically.
5. Turn the fan relay ON/OFF based on temperature thresholds.
6. Turn the lamp relay ON/OFF based on light level.
7. Use RGB LED to show temperature status:
   - **Red blink** = hot
   - **Blue** = low temperature
   - **Green** = normal range
8. When authorization is revoked, turn off relays and indicators.

### ESP32 Drowsiness Monitor
1. Power on the ESP32.
2. Connect to Wi-Fi.
3. Connect to the MQTT broker.
4. Subscribe to `led/control`.
5. Receive alert values and update LEDs.
6. Reconnect if the MQTT link drops.

---

## 📌 Pin Connections

### ESP8266 RFID Room Control
| Signal | NodeMCU Pin | Description |
|---|---|---|
| Fan relay | D1 | Fan control output |
| Lamp relay | D2 | Lamp control output |
| DHT11 data | D5 | Sensor data input |
| LDR | A0 | Ambient light analog input |
| RGB Red | D8 | PWM red output |
| RGB Green | D6 | PWM green output |
| RGB Blue | D7 | PWM blue output |

### ESP32 Drowsiness Monitor
| Signal | ESP32 Pin | Description |
|---|---|---|
| Red LED | GPIO 26 | Warning LED output |
| Green LED | GPIO 27 | Status LED output |

---

## ⚙️ Setup Instructions

### 1. Prepare the environment
- Install Arduino IDE or PlatformIO.
- Install ESP8266 and ESP32 board support packages.
- Install libraries:
  - `DHT` for ESP8266
  - `PubSubClient` for ESP32

### 2. Open the correct project
- ESP8266: `ESP8266-RFID-Room-Control/ESP8266-RFID-Room-Control.ino`
- ESP32: `ESP32-Drowsiness-Monitor/ESP32-Drowsiness-Monitor.ino`

### 3. Configure the sketch
- Update Wi-Fi SSID/password in the ESP32 sketch if needed.
- Confirm the ESP8266 ESP-NOW sender and receiver use the same message struct.

### 4. Upload the sketch
- Select the correct board type and COM port.
- Upload the sketch.
- Open Serial Monitor to confirm the startup messages.

---

## ✅ Recommended Steps

1. Wire the hardware from `HARDWARE.md`.
2. Verify all sensor and LED connections.
3. Upload the chosen sketch.
4. Open Serial Monitor for diagnostics.
5. Test ESP-NOW authorization for the RFID project.
6. Test MQTT messages for the drowsiness monitor.

---

## 💡 Best Practices

- Keep Wi-Fi credentials out of public code.
- Use resistors with LEDs.
- Use a dedicated power source for relays.
- Keep wiring short and secure.
- Test each module before performing full integration.

---

## Additional Documentation

- `CONTRIBUTING.md` — how to contribute.
- `HARDWARE.md` — wiring and hardware details.
- `LICENSE` — MIT license.

---

## 📄 License

This project is licensed under the MIT License. See `LICENSE` for details.