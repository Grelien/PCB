
This repository contains the schematic design for a custom **ESP32-S3-WROOM-1** based control board.  
The design integrates safe **AC to DC conversion**, **power management**, **battery charging**, and an **optocoupler-isolated driver** for controlling external devices such as solenoid valves — all on a single PCB.

---

## 📘 Overview

The board uses the **ESP32-S3-WROOM-1 (N8R8)** module as the main microcontroller, with onboard Wi-Fi and Bluetooth connectivity.  
It includes a **CP2102N** USB-C-to-UART interface for programming and serial communication, a **TPS54302** buck converter for stable 3.3 V power, and a **TP4056** battery charger with protection circuitry.

---

## ⚙️ Key Features

- **MCU:** ESP32-S3-WROOM-1 (8 MB Flash, 8 MB PSRAM)  
- **USB Interface:** Single CP2102N USB-to-UART bridge  
  - Used for programming and serial communication  
  - Provides 5 V power input from USB  
- **AC to DC Power Supply:**
  - **HLK-5M05** module converts **230 V AC → 5 V DC**
  - Input protected by fuse **F1**
  - Output filtered with capacitors and EMI inductor
- **DC-DC Converter:**
  - **TPS54302** step-down regulator converts **5 V → 3.3 V** for the ESP32
- **Battery Management:**
  - **TP4056** Li-ion charger with **DW01A + FS8205A** protection ICs
  - Battery connector (J3) for single-cell Li-ion/Li-poly battery
- **Optocoupler Output Driver:**
  - **PC817C** isolation optocoupler  
  - **2N2222** NPN transistor for solenoid/relay control  
  - **D10 (1N4007)** flyback diode for inductive load protection  
  - **GPIO9** used for control signal
- **User Interface:**
  - **RESET** and **BOOT** push buttons  
  - **Two status LEDs** (Blue & Green)

---

## ⚡ Power Architecture

| Stage | Input | Output | Component | Description |
|--------|--------|---------|------------|--------------|
| AC-DC | 230 V AC | 5 V DC | HLK-5M05 | Mains converter |
| DC-DC | 5 V | 3.3 V | TPS54302 | Buck converter |
| Battery | USB/5 V | 3.7 V cell | TP4056 + DW01A | Charger & protection |
| MCU Power | 3.3 V | – | ESP32-S3 | Logic supply |

⚠️ **Safety Note:** The HLK-5M05 module operates directly from 230 V AC.  
Use proper creepage/clearance, fuse protection, and a non-conductive enclosure when testing or deploying the board.

---

## 🔌 Connectors

| Connector | Function | Notes |
|------------|-----------|-------|
| **CN1** | AC Input (L_IN, N_IN) | 230 V AC to HLK-5M05 |
| **CN2** | DC Output (+VO, -VO) | 5 V DC output from converter |
| **J3** | Battery Connector (B+, B-) | Connect single-cell Li-ion |
| **USB** | Power + UART | CP2102N interface for power and programming |

---

## 🧩 Main Components

| Reference | Component | Description |
|------------|------------|-------------|
| **U1** | ESP32-S3-WROOM-1 | Main microcontroller |
| **U2** | CP2102N-A02-GQFN28 | USB-to-UART bridge |
| **U10** | TPS54302DDCR | 5 V → 3.3 V step-down converter |
| **U9** | TP4056 | Li-ion battery charger |
| **U8** | DW01A + FS8205A | Battery protection ICs |
| **U11** | HLK-5M05 | 230 V AC to 5 V DC converter |
| **U12** | PC817C | Optocoupler for load isolation |
| **Q6** | 2N2222 | Solenoid/relay driver transistor |
| **D10** | 1N4007 | Flyback protection diode |
| **R29/R30** | 330 Ω / 10 kΩ | Optocoupler LED and pull-up resistors |
| **LED1–LED2** | Blue/Green LEDs | Power and status indicators |
| **SW2/SW3** | Push buttons | BOOT and RESET |

---

## 🧠 Functional Blocks

1. **Power Supply Section:** Converts 230 V AC to 5 V DC, then 3.3 V for MCU  
2. **Battery Management:** Charges and protects a single Li-ion cell  
3. **MCU Section:** ESP32-S3 with USB programming, reset, and boot control  
4. **Optocoupler Driver:** Isolated control for external solenoid or relay  
5. **Indicator Section:** Two LEDs for system status  

---

## 🛠️ Design Information

| Field | Value |
|-------|--------|
| **File Name** | `SCH_ESP32_2025-10-26.pdf` |
| **Revision** | 1.0 |
| **Date** | 2025-09-14 |
| **Designer** | Hemakanth N |
| **Company** | Grelien |

---

## 📂 Repository Contents

| File | Description |
|------|-------------|
| `SCH_ESP32_2025-10-26.pdf` | Schematic diagram of the ESP32-S3 control board |
| `README.md` | Detailed board documentation |

---

## 🚀 Future Enhancements

- Add **PCB layout** and **Gerber files**  
- Include **firmware example** for optocoupler control via GPIO9  
- Optional: integrate **ADC-based battery voltage monitor**

---

## 📄 License

This design is provided for **educational and prototyping purposes**.  
For commercial use or derivative works, please credit the original designer.

---

**© 2025 Grelien 
