# Wi-Fi in Embedded Systems

**Wi-Fi (Wireless Fidelity)** is a wireless networking technology that enables devices to communicate over a local area network (LAN) or access the internet using IEEE 802.11 standards. It's a high-throughput, IP-based protocol commonly used in embedded systems that require cloud connectivity or high-speed local data exchange.

---

## Wi-Fi Basics

| Feature             | Description                                      |
|---------------------|--------------------------------------------------|
| Standard            | IEEE 802.11 (a/b/g/n/ac/ax)                      |
| Frequency Bands     | 2.4 GHz, 5 GHz (and 6 GHz in Wi-Fi 6E)           |
| Data Rates          | Up to 600 Mbps (802.11n), >1 Gbps (802.11ac/ax)  |
| Range               | ~50 m indoor, up to 100 m outdoor                |
| Security            | WPA2, WPA3 encryption                            |

---

## Common Wi-Fi Modes in Embedded

| Mode         | Description                                                |
|--------------|------------------------------------------------------------|
| **Station**  | Connects to an access point (AP) like a smartphone does   |
| **Soft AP**  | Acts as an access point, allowing others to connect       |
| **P2P/Ad-Hoc** | Peer-to-peer communication without AP                   |

---

## Applications

| Application                | Example                                |
|----------------------------|----------------------------------------|
| IoT Cloud connectivity     | Smart home sensors with cloud upload   |
| Web server for config      | ESP32-based device serving config page |
| OTA updates                | Firmware updates via internet          |
| Wireless data streaming    | Camera modules, audio streaming        |

---

## Popular Wi-Fi Modules/Chips

- **ESP8266**, **ESP32** – Very popular with built-in TCP/IP stack
- **WILC1000**, **CC3200**, **Nina-W10**, **RTL8720** – Used in industrial products
- Many modules support both **Wi-Fi + BLE** combo

---

## Security Considerations

- Use **WPA2/WPA3** encryption
- Avoid exposing open networks in production
- Implement **HTTPS**, **TLS**, or **MQTT with TLS** for secure communication
