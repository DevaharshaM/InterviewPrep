# TCP/IP Model – Transmission Control Protocol/Internet Protocol

The **TCP/IP model** is the foundation of modern networking. It simplifies communication by breaking the network stack into **4 layers**, each handling a specific task in the transmission of data.

---

## TCP/IP Model

<figure>
 <img src="https://github.com/DevaharshaM/InterviewPrep/blob/microController/Networking%20%26%20Connectivity/tcp.png">
 <figcaption>Figure 1: TCP/IP Layers</figcaption>
</figure>

---

## TCP/IP Layers Overview

| Layer                | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| **Application Layer** | Provides protocols for software to communicate (e.g., HTTP, FTP, DNS)       |
| **Transport Layer**   | Ensures reliable or fast delivery (TCP for reliability, UDP for speed)      |
| **Internet Layer**    | Responsible for logical addressing and routing (e.g., IP, ICMP)             |
| **Network Access Layer** | Deals with the physical transmission of data (e.g., Ethernet, Wi-Fi)     |

---

## Comparison with OSI Model

| OSI Layer               | TCP/IP Equivalent         |
|-------------------------|---------------------------|
| Application, Presentation, Session | Application Layer |
| Transport               | Transport Layer            |
| Network                 | Internet Layer             |
| Data Link + Physical    | Network Access Layer       |

---

## Key Protocols by Layer

| Layer               | Example Protocols        |
|---------------------|--------------------------|
| Application         | HTTP, HTTPS, FTP, SMTP   |
| Transport           | TCP, UDP                 |
| Internet            | IP, ICMP, IGMP           |
| Network Access      | Ethernet, Wi-Fi, ARP     |

---

## Notes

- **TCP**: Connection-oriented, reliable (ensures data is received and in order)
- **UDP**: Connectionless, faster, but no delivery guarantee
- **IP**: Handles addressing and routing between hosts

---

## Summary

The TCP/IP model is practical, protocol-based, and forms the backbone of all internet communication. It maps closely with real-world protocol implementations.
