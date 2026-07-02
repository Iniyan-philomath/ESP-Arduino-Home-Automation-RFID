# Hardware and Wiring Guide

This guide describes the hardware setup for both ESP projects in the repository.

## ESP8266 RFID Room Control

### Components
- ESP8266 NodeMCU
- DHT11 sensor
- LDR light sensor
- 2-channel relay module
- RGB LED or three separate indicator LEDs
- ESP-NOW sender device / card scanner

### Wiring

| Component | NodeMCU Pin | Notes |
|---|---|---|
| Fan relay IN | D1 | Relay control for fan |
| Lamp relay IN | D2 | Relay control for lamp |
| DHT11 data | D5 | DHT11 sensor signal pin |
| LDR | A0 | Analog light sensor input |
| RGB red | D8 | PWM output for red channel |
| RGB green | D6 | PWM output for green channel |
| RGB blue | D7 | PWM output for blue channel |

### Power
- Use a stable 5V supply for NodeMCU.
- Provide separate power for relays if needed.
- Common ground is required between the NodeMCU and relay module.

## ESP32 Drowsiness Monitor

### Components
- ESP32 development board
- Red LED
- Green LED
- 220Ω resistors

### Wiring

| Component | ESP32 Pin | Notes |
|---|---|---|
| Red LED | GPIO 26 | Connect through resistor to ground |
| Green LED | GPIO 27 | Connect through resistor to ground |

### Power
- Use the onboard USB power or a 5V power supply.
- Make sure the board is properly grounded.

## Best Practices

- Avoid powering relays directly from the development board pins.
- Use a relay driver module or transistor stage if your relay board requires more current.
- Keep wires short and secure to reduce noise and false triggers.
- Double-check your pin connections before uploading the sketch.