# ESP8266 RFID Room Control System

## Overview

This project implements a secure room automation system using an ESP8266 NodeMCU as an ESP-NOW receiver. The system controls fans and lamps based on temperature and light levels while maintaining strict authorization through ESP-NOW protocol.

## Features

✅ **ESP-NOW Authorization** - Secure wireless authentication  
✅ **Temperature Control** - DHT11 sensor with relay activation  
✅ **Light Sensing** - LDR for ambient light detection  
✅ **RGB LED Status** - Visual feedback for system state  
✅ **Automatic Relay Control** - Fan and lamp management  
✅ **Safety Shutdown** - Disables outputs when unauthorized  

## Hardware Requirements

- ESP8266 NodeMCU
- DHT11 Temperature/Humidity Sensor
- LDR (Light Dependent Resistor)
- 2-Channel Relay Module
- RGB LED (or 3 individual LEDs)
- ESP-NOW sender device
- 5V stable power supply

## Pin Configuration

| Component | Pin | Function |
|-----------|-----|----------|
| Fan Relay | D1 | Relay control |
| Lamp Relay | D2 | Relay control |
| DHT11 | D5 | Data pin |
| LDR | A0 | Analog input |
| RGB Red | D8 | Red LED |
| RGB Green | D6 | Green LED |
| RGB Blue | D7 | Blue LED |

## Setup Instructions

1. **Install Libraries**
   - Open Arduino IDE → Sketch → Include Library → Manage Libraries
   - Search and install: `DHT sensor library by Adafruit`

2. **Configure Board**
   - Select Board: ESP8266 NodeMCU 1.0
   - Set Baud Rate: 115200
   - Select COM Port

3. **Upload Sketch**
   - Open `ESP8266-RFID-Room-Control.ino`
   - Click Upload

4. **Serial Monitor**
   - Open Serial Monitor (115200 baud)
   - Verify startup messages

## Operation

### Startup Sequence
1. ESP8266 initializes ESP-NOW
2. Waits for authorization packet from sender
3. RGB LED shows blue (waiting)

### Authorized Mode
- RGB LED shows green (normal operation)
- Continuously reads DHT11 and LDR
- Controls relays based on thresholds
- Sends periodic status updates

### Status Indicators
- 🟢 **Green** = Normal temperature range
- 🔴 **Red Blink** = High temperature (fan ON)
- 🔵 **Blue** = Low temperature
- 🟡 **Yellow** = Low light (lamp ON)

## Thresholds (Configurable)

```cpp
const int TEMP_HIGH = 30;      // °C - activate fan
const int TEMP_LOW = 15;       // °C - show blue
const int LIGHT_THRESHOLD = 500; // LDR analog value
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Not receiving ESP-NOW | Verify sender MAC address in code |
| DHT11 not reading | Check D5 connection, use 4.7kΩ resistor |
| Relay not activating | Check D1/D2 pins, verify relay module power |
| LED not lighting | Verify resistors (220Ω recommended) |
| Serial monitor shows garbage | Check baud rate (115200) |

## Future Enhancements

- [ ] Web dashboard for remote control
- [ ] MQTT integration
- [ ] Scheduling system
- [ ] Multiple room support
- [ ] Energy monitoring

## License

MIT License - See LICENSE file
