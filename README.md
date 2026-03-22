# SmartResQ — IoT–Cloud–Web Integrated System for Smart Ambulance Route Clearance

> A research prototype that automates ambulance lane clearance using IoT smart poles, cloud backend, and a real-time web interface — achieving <2.2s end-to-end latency.

---

## Abstract

Emergency response time is a critical factor in patient survival. In dense urban areas, ambulances face severe traffic congestion, leading to delayed arrivals. Existing systems rely on manual oversight or isolated GPS tracking without unified automation.

**SmartResQ** addresses this by integrating a React-based web interface, a Node.js–Express cloud backend, and IoT-enabled smart poles (EC200U GSM + ESP32) retrofitted on existing streetlight infrastructure. When an ambulance activates emergency mode, the system computes the optimal route, identifies all registered smart poles along the path, and sends real-time activation signals — triggering LED and buzzer alerts to clear the lane — within 2 seconds.

**Prototype results:** 98% pole activation accuracy · <2.2s signal latency · 96% network uptime · ~60% reduction in manual coordination delay.

---

## Research Paper

**Title:** SmartResQ: IoT–Cloud–Web Integrated System for Smart Ambulance Route Clearance

**Authors:** Nadeem, Chhavi, Shubham Kumar, Dev Varshney

**Advisors:** Dr. Vineet Shrivastava, Dr. Devesh Garg

**Institution:** Raj Kumar Goel Institute of Technology, Ghaziabad

**Status:** Under review / conference submission (IEEE format)

> Paper presented as PPT. Journal submission in progress.

---

## System Architecture

```
Ambulance Driver
      │
      ▼
 React Web App              ← Emergency mode trigger + live GPS capture
      │  (HTTPS)
      ▼
 Node.js–Express Backend    ← Route computation (Google Maps API)
      │                        Pole identification (MongoDB lookup)
      │  (GSM)
      ▼
 EC200U GSM Module          ← Receives activation signal from cloud
      │  (UART)
      ▼
 ESP32 Microcontroller      ← Triggers LED flasher + buzzer alert
      │
      ▼
 Lane Cleared ✓

      +── MongoDB ──────── Stores GPS, pole state, event logs
      +── React Dashboard ─ Live ambulance position + pole status
```

---

## Tech Stack

### Software

| Layer | Technology | Role |
|---|---|---|
| Frontend | React.js | Driver interface + monitoring dashboard |
| Backend | Node.js + Express | Cloud logic, route mapping, pole activation |
| Database | MongoDB | Real-time GPS data, pole registry, event logs |
| Maps | Google Maps API | Optimal route computation |
| Testing | Postman, Node-RED | API validation, data flow monitoring |
| Simulation | TinkerCAD | Circuit-level verification |

### Hardware

| Component | Model | Function |
|---|---|---|
| Microcontroller | ESP32 | Processes GSM commands, controls outputs |
| GSM Module | EC200U | Receives cloud activation signals |
| Alert System | LED + Buzzer | Visual and audible lane-clearing alerts |
| Power Supply | 5V DC Regulated | Powers ESP32 and peripherals |

---

## Key Results

| Metric | Observed Value | Remarks |
|---|---|---|
| Data Transmission Delay | 1.8 – 2.2 seconds | Backend → EC200U → ESP32 |
| Pole Activation Accuracy | 98% | Across all test events |
| Dashboard Update Latency | < 1 second | Near real-time display |
| Network Reliability | 96% uptime | Stable GSM signal handling |
| Response Time Reduction | ~60% faster | vs. traditional manual methods |

---

## Comparative Advantage

| Feature | Traditional Systems | SmartResQ |
|---|---|---|
| Lane clearance trigger | Manual / human-operated | Fully automated via cloud |
| Latency per signal node | 5–10 seconds | < 2.2 seconds |
| Infrastructure needed | New hardware installations | Retrofits existing streetlights |
| Scalability | Limited | Add poles via MongoDB entry |
| Multi-ambulance support | No | Yes, parallel operation |

---

## Getting Started

### Prerequisites
- Node.js v18+
- MongoDB Atlas or local MongoDB
- Arduino IDE (for ESP32 firmware)
- EC200U GSM module with active SIM

### Backend Setup

```bash
git clone https://github.com/dev200413y/smartresq
cd smartresq/backend
npm install
cp .env.example .env   # Add MongoDB URI + Google Maps API key
node server.js
```

### Frontend Setup

```bash
cd ../frontend
npm install
npm start
```

### ESP32 Firmware

Flash `firmware/smartpole.ino` via Arduino IDE to each ESP32 unit. Configure the GSM APN and backend endpoint in `config.h`.

---

## Future Scope

- [ ] AI-based route prediction using real-time traffic data
- [ ] 5G / LoRa fallback communication for weak GSM zones
- [ ] Edge computing integration for reduced cloud dependency
- [ ] Multi-city deployment with centralized dashboard
- [ ] Integration with hospital arrival notification system

---

## Authors

| Name | Institution | Contact |
|---|---|---|
| Nadeem | RKGIT, Ghaziabad | nadeemsiddiqui0390@gmail.com |
| Chhavi | RKGIT, Ghaziabad | chhavirathi246@gmail.com |
| Shubham Kumar | RKGIT, Ghaziabad | shubhu2809as@gmail.com |
| Dev Varshney | RKGIT, Ghaziabad | varshney.dev.013@gmail.com |

**Faculty Advisors:** Dr. Vineet Shrivastava · Dr. Devesh Garg

---

## Citation

```
Nadeem, Chhavi, Shubham Kumar, Dev Varshney, "SmartResQ: IoT–Cloud–Web 
Integrated System for Smart Ambulance Route Clearance," Raj Kumar Goel 
Institute of Technology, Ghaziabad, 2025. (Under Review)
```

---

## License

MIT License — see [LICENSE](LICENSE) for details.
