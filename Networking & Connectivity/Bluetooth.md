# Bluetooth in Embedded Systems

**Bluetooth** is a short-range wireless communication protocol designed for low-power, low-cost data exchange between devices. It operates in the 2.4 GHz ISM band and is widely used in embedded systems for applications like sensor communication, audio streaming, and device control.

---

## Bluetooth Basics

| Feature             | Description                                              |
|---------------------|----------------------------------------------------------|
| Frequency Band      | 2.4 GHz ISM                                              |
| Range               | Typically 10 m (Class 2), up to 100 m (Class 1)          |
| Topology            | Point-to-point, Star (Piconet), Scatternet               |
| Data Rate           | Classic: Up to 3 Mbps, BLE: Up to 2 Mbps                 |
| Power Consumption   | BLE is optimized for ultra-low power                     |

---

## Bluetooth Versions

| Version   | Key Feature Highlights                        |
|-----------|-----------------------------------------------|
| 2.0 + EDR | Faster data rates (up to 3 Mbps)              |
| 4.0       | Introduced Bluetooth Low Energy (BLE)         |
| 5.0       | Higher speed (2 Mbps), longer range, more robust |
| 5.1/5.2   | Direction finding, audio improvements (LE Audio) |

---

## Classic Bluetooth vs BLE

| Feature         | Classic Bluetooth     | Bluetooth Low Energy (BLE)     |
|------------------|------------------------|---------------------------------|
| Power            | Higher                 | Ultra-low                      |
| Latency          | Low                    | Slightly higher                |
| Throughput       | Higher (~2-3 Mbps)     | Lower (up to 2 Mbps)           |
| Use Case         | Audio, File Transfer   | Sensors, IoT, Wearables        |
| Connection       | Persistent             | Can be intermittent            |

---

## Bluetooth Architecture

- **Piconet**: One master + up to 7 active slave devices
- **Scatternet**: Multiple piconets interconnected
- **Profiles**: Define use cases (e.g., A2DP for audio, HID for input devices)

---

## BLE Communication Process

1. **Advertising**: Devices broadcast availability
2. **Scanning**: Devices listen for advertisements
3. **Connection**: Central initiates connection with peripheral
4. **GATT Communication**: Services & Characteristics define data exchange

---

## Applications

| Application               | Notes                                        |
|---------------------------|-----------------------------------------------|
| Wireless sensors          | BLE for battery-powered temperature, motion  |
| Device pairing            | Keyboards, mice, controllers                  |
| Audio streaming           | Classic Bluetooth (e.g., A2DP)               |
| Mobile control interfaces | BLE apps to control embedded devices         |

Popular modules: **HC-05**, **HC-06**, **nRF52**, **ESP32**, **BlueNRG**
