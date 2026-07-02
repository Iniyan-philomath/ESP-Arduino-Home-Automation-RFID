# ESP32 Drowsiness Monitor System

## Overview

This project implements an MQTT-based drowsiness alert monitoring system using an ESP32 board. The system receives alerts through MQTT and displays warnings via LED indicators.

## Features

✅ **MQTT Integration** - Real-time alert reception  
✅ **LED Status Indicators** - Red and Green LEDs for alerts  
✅ **Wi-Fi Connectivity** - Automatic connection management  
✅ **Auto-Reconnect** - Reconnects if connection drops  
✅ **Topic Subscription** - Listens to `led/control` topic  
✅ **Low-Power Design** - Efficient GPIO control  

## Hardware Requirements

- ESP32 Development Board
- Red LED
- Green LED
- 2× 220Ω Resistors
- USB power supply or 5V regulator

## Pin Configuration

| Component | ESP32 Pin | Function |
|-----------|-----------|----------|
| Red LED | GPIO 26 | Warning indicator |
| Green LED | GPIO 27 | Status indicator |
| GND | GND | Common ground |

## Setup Instructions

1. **Install Board Support**
   - Arduino IDE → Preferences → Additional Board URLs
   - Add: `https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json`
   - Board Manager → Search and install: `esp32`

2. **Install Libraries**
   - Sketch → Include Library → Manage Libraries
   - Search and install: `PubSubClient by Nick O'Leary`

3. **Configure Credentials**
   ```cpp
   const char* ssid = "YOUR_SSID";
   const char* password = "YOUR_PASSWORD";
   const char* mqtt_server = "YOUR_MQTT_BROKER_IP";
   ```

4. **Upload Sketch**
   - Select Board: ESP32 Dev Module
   - Set Baud Rate: 115200
   - Click Upload

5. **Monitor Connection**
   - Open Serial Monitor (115200 baud)
   - Watch for Wi-Fi and MQTT connection messages

## Operation

### Startup Sequence
1. Initialize GPIO pins
2. Connect to Wi-Fi network
3. Connect to MQTT broker
4. Subscribe to `led/control` topic
5. Green LED blinks (ready)

### Alert Levels

**MQTT Message Format:** `topic: led/control` → `payload: [0-2]`

| Value | Alert Level | LED Behavior |
|-------|-------------|---------------|
| 0 | No Alert | Green ON, Red OFF |
| 1 | Mild Alert | Green blink |
| 2 | Critical Alert | Red blink, Green OFF |

### Message Publishing Example

```bash
# Using MQTT CLI
mosquitto_pub -h broker.ip -t led/control -m "2"

# Critical drowsiness alert
```

## MQTT Configuration

### Broker Settings
- **Host:** Your MQTT broker IP (e.g., 192.168.1.100)
- **Port:** 1883 (default)
- **Topic:** `led/control`
- **QoS:** 0 or 1

### Recommended MQTT Brokers
- Mosquitto (local/self-hosted)
- HiveMQ Cloud (free tier)
- Adafruit IO (IoT platform)

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Won't connect to Wi-Fi | Check SSID/password, verify network |
| MQTT connection fails | Verify broker IP, check firewall |
| LEDs not lighting | Check GPIO 26/27, verify resistor connections |
| No MQTT messages received | Subscribe to topic, verify publish |
| Serial shows random characters | Check baud rate (115200) |

## Customization

### Change LED Pins
```cpp
#define RED_LED 26    // Change to your pin
#define GREEN_LED 27  // Change to your pin
```

### Modify Alert Thresholds
```cpp
// In callback function
if (payload_int == 2) { // Critical
  // Your custom action
}
```

## Future Enhancements

- [ ] Web dashboard
- [ ] Mobile app notifications
- [ ] Buzzer/alarm integration
- [ ] Data logging to cloud
- [ ] Multi-device support
- [ ] AI-based drowsiness detection

## License

MIT License - See LICENSE file
