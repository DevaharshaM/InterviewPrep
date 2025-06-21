# OSI Model – Open Systems Interconnection

The **OSI Model** is a conceptual framework used to understand how data is transmitted over a network. It divides the networking process into **7 layers**, each responsible for specific functions.

---

## OSI Model 

<figure>
 <img src ="https://github.com/DevaharshaM/InterviewPrep/blob/microController/Networking%20%26%20Connectivity/osi.png">
 <figcaption>Figure 1: OSI Layers</figcaption>
</figure>

---

## OSI Layers Explained

| Layer | Name               | Purpose |
|-------|--------------------|---------|
| 7     | **Application**    | Interface for user applications (e.g., browsers, FTP clients) |
| 6     | **Presentation**   | Data formatting, encryption, compression |
| 5     | **Session**        | Manages sessions and connections |
| 4     | **Transport**      | End-to-end delivery, segmentation, flow control (e.g., TCP, UDP) |
| 3     | **Network**        | Logical addressing and routing (e.g., IP) |
| 2     | **Data Link**      | MAC addressing, framing, error detection (e.g., Ethernet, Wi-Fi) |
| 1     | **Physical**       | Transmission of raw bits over medium (e.g., cables, voltage) |

---

## Key Notes

- Data travels **from Layer 7 to 1 on the sender side** and **Layer 1 to 7 on the receiver side**.
- Common protocols operate at different layers:
  - HTTP (Layer 7)
  - SSL/TLS (Layer 6)
  - TCP/UDP (Layer 4)
  - IP (Layer 3)
  - Ethernet/Wi-Fi (Layer 2)
- **Encapsulation** occurs at each layer to add headers relevant for processing.

---

## Real-World Analogy

| Step                | OSI Layer       |
|---------------------|------------------|
| You writing a message | Application (7) |
| Translating language  | Presentation (6) |
| Starting conversation | Session (5) |
| Speaking clearly      | Transport (4) |
| Addressing message    | Network (3) |
| Packaging and envelope| Data Link (2) |
| Sending it via post   | Physical (1) |

---

# Summary

The OSI model helps developers design, troubleshoot, and understand communication systems by breaking the complex process into manageable layers.
