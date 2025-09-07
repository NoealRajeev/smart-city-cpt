# Smart City using Cisco Packet Tracer

## Table of Contents

* [Aim](#aim)
* [Problem Statement](#problem-statement)
* [Scope of the Solution](#scope-of-the-solution)
* [System Overview & Architecture](#system-overview--architecture)
* [Required Components](#required-components)
  * [Software / IDEs](#software--ides)
  * [Hardware (Simulated)](#hardware-simulated)
* [Network Topology](#network-topology)
* [Module Design](#module-design)
  * [Smart Surveillance](#1-smart-surveillance)
  * [Intelligent Street Lighting](#2-intelligent-street-lighting)
  * [Fire Monitoring](#3-fire-monitoring)
* [Repository Structure](#repository-structure)
* [Getting Started](#getting-started)
  * [Open the Simulation](#open-the-simulation)
  * [Run the Demo](#run-the-demo)
* [Screenshots & Demo Video](#screenshots--demo-video)
* [Evaluation Checklist](#evaluation-checklist)
* [How We Built It (Steps & Commands)](#how-we-built-it-steps--commands)
* [Contributing & Branching](#contributing--branching)
* [License](#license)
* [Acknowledgements](#acknowledgements)
* [Team](#team)

---

## Aim

Design and simulate an **intelligent urban environment** in **Cisco Packet Tracer** integrating:

1. **Smart Surveillance**, 2) **Intelligent Street Lighting**, and 3) **Fire Monitoring**,  
   with centralized monitoring and basic automation rules.

## Problem Statement

Urban services often operate in silos with limited visibility. The goal is to build a simulated **Smart City** network where **IoT sensors/actuators** and **IP surveillance** devices are connected via a managed network to an **IoT Server/Controller** and **Dashboard**, enabling:

* Real-time monitoring
* Rule-based automation (event → action)
* Fault tolerance and manageable addressing

## Scope of the Solution

* **In scope**
  * End-to-end simulation using Cisco Packet Tracer (PT IoT components)
  * Device addressing, routing/switching, and wireless access as needed
  * Three functional subsystems with event triggers and visible outcomes
  * Basic dashboard/monitoring via PT IoT Server or Web Panel

* **Out of scope**
  * External cloud services beyond Packet Tracer
  * Production-grade video analytics (we simulate motion/alerts)

---

## System Overview & Architecture

**Layers:**

* **Perception:** Cameras, motion sensors, LDRs, smoke/temperature sensors; street lights and alarms as actuators  
* **Network:** Access switches, wireless APs, routers, DHCP server; optional VLANs per subsystem  
* **Application/Control:** PT **IoT Server** hosting rules (if-This-Then-That), data logging, and a web dashboard  

**Automation Rules (examples):**

* *If* motion detected near camera after 22:00 → *Then* turn street light **ON** and log event  
* *If* smoke > threshold → *Then* trigger **Alarm** and notify dashboard  

---

## Required Components

### Software / IDEs

* **Cisco Packet Tracer (8.2.1+ recommended)**
* (Optional) **Tinkercad** or **Fritzing** — schematic illustration
* (Optional) **OBS Studio** / screen recorder — for demo video capture
* (Optional) **VS Code** — to edit README and markdown assets

### Hardware (Simulated)

*(All devices below are **Packet Tracer IoT** / networking elements.)*

* **Routers** (1–2) and **Switches** (2–3)
* **Wireless Access Point** (if using Wi-Fi IoT)
* **IoT Server** (PT)
* **End Host** (PC/Laptop) for monitoring
* **Smart Cameras** (IP Camera or simulated motion + camera combo)
* **Motion Sensors**
* **LDR/Light Sensors** + **Smart Street Lights** (actuators)
* **Smoke/Temperature Sensors** + **Fire Alarm/Buzzer** (actuator)

> **Note:** The exact device names vary by PT version (e.g., *Home Gateway*, *Server-PT*, *IoT Camera*, *Smart Light*, etc.).

---

## Network Topology

* **Core**: 1 Router providing inter-VLAN routing/DHCP (or dedicated DHCP server)  
* **Access**: 2 Switches (one for surveillance & lighting, one for fire system)  
* **Wireless**: 1 AP for wireless sensors (optional — otherwise use wired IoT)  
* **Addressing** (example):
  * VLAN 10 – Surveillance: `192.168.10.0/24`
  * VLAN 20 – Street Lighting: `192.168.20.0/24`
  * VLAN 30 – Fire Monitoring: `192.168.30.0/24`
  * IoT Server: `192.168.99.10`

---

## Module Design

### 1) Smart Surveillance
* **Devices:** IP Camera(s), Motion Sensor(s)  
* **Flow:** Motion → Camera records (simulated) → Event to IoT Server → Log & Indicator on dashboard  
* **Rule:** Motion detected between 22:00–05:00 ⇒ log *SecurityEvent* and toggle indicator LED  

### 2) Intelligent Street Lighting
* **Devices:** LDR (Light Sensor), Smart Street Light(s)  
* **Flow:** LDR reads ambient light → Controller decides → Street Light ON/OFF  
* **Rule:** If ambient light < threshold *or* motion at night ⇒ turn ON nearest street lights  

### 3) Fire Monitoring
* **Devices:** Smoke/Temp Sensors, Alarm/Buzzer  
* **Flow:** Threshold breach → IoT Server rule → Alarm ON + alert message to dashboard  
* **Rule:** Smoke > X *or* Temp > Y ⇒ Trigger siren; restore when normal  

---

## Repository Structure

```

smart-city-cpt/
├─ .github/
│  ├─ ISSUE\_TEMPLATE/
│  │  ├─ bug\_report.md
│  │  └─ feature\_request.md
│  └─ workflows/
│     └─ markdown-lint.yml
├─ assets/
│  ├─ screenshots/
│  │  ├─ topology.png
│  │  ├─ surveillance-demo.png
│  │  ├─ street-lighting-demo.png
│  │  └─ fire-monitoring-demo.png
│  ├─ diagrams/
│  │  └─ architecture.drawio
│  └─ video/
│     └─ demo.mp4
├─ simulation/
│  └─ smart\_city.pkt
├─ docs/
│  └─ report.pdf
├─ README.md
├─ LICENSE
└─ .gitignore

````

---

## Getting Started

### Open the Simulation
1. Install **Cisco Packet Tracer** (8.2.1 or later) and launch it.  
2. `File → Open` → load `simulation/smart_city.pkt`.  
3. Wait for devices to boot; confirm IPs/DHCP leases if applicable.  

### Run the Demo
1. Open the **IoT Server Dashboard** (or Web UI) and verify devices are **Online**.  
2. **Surveillance:** Toggle a **motion sensor** near the camera → check dashboard log/indicator.  
3. **Street Lighting:** Reduce **LDR** value (simulate night) → lights should turn **ON** automatically.  
4. **Fire Monitoring:** Increase **smoke/temp** sensor values beyond threshold → **Alarm** should trigger.  
5. Capture screenshots and a **short demo video** (2–3 min).  

> Tip: In PT, use the **Realtime** tab for steady state and **Simulation** tab to visualize events.  

---

## Screenshots & Demo Video

* Topology: `assets/screenshots/topology.png`  
* Surveillance: `assets/screenshots/surveillance-demo.png`  
* Street Lighting: `assets/screenshots/street-lighting-demo.png`  
* Fire Monitoring: `assets/screenshots/fire-monitoring-demo.png`  

**Demo Video:**  
* Add `assets/video/demo.mp4` **or** upload via **GitHub Releases** and paste the link here.  

---

## Evaluation Checklist

* [ ] **Aim** clearly stated  
* [ ] **Problem Statement** and **Scope** covered  
* [ ] **Packet Tracer file** included and opens without errors  
* [ ] **Three subsystems** implemented and demonstrable  
* [ ] **Automation rules** configured on IoT Server  
* [ ] **Screenshots** included  
* [ ] **Demo video** added  
* [ ] **README** updated with team details  

---

## How We Built It (Steps & Commands)

**Git Initialization**
```bash
git init
git remote add origin https://github.com/NoealRajeev/smart-city-cpt.git
````

**Recommended `.gitignore`**

```
# OS
.DS_Store
Thumbs.db

# Editors
.vscode/
.idea/

# Media/exports
assets/video/*
!assets/video/README.md
```

**LICENSE**: MIT
**Issue Templates**: in `.github/ISSUE_TEMPLATE/`

---

## Contributing & Branching

* **Default branch:** `main`
* **Feature branches:** `feature/<module-name>` (e.g., `feature/fire-monitoring`)
* **Commit style:** short imperative messages
* **PR Review:** 1 teammate review before merge

---

## License

This project is licensed under the **MIT License** — see `LICENSE` for details.

---

## Team

* **2362523 - Noeal Rajeev Thaleeparambil**
* **2362524 - Noel John**
* **2362525 - Pamuru Ritesh Reddy**
* **2362526 - Pawan K Das**
* **2362527 - Pius Binu**
