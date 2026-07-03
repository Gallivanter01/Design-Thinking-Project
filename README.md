# Rural Bus Tracking and Passenger Information System

[cite_start]An off-grid, low-power, and scalable transit intelligence solution designed to provide real-time bus arrival information in rural areas without the need for cellular networks or internet connectivity[cite: 30, 68].

## 🔧 System Architecture
[cite_start]The system employs a distributed architecture utilizing three specialized hardware units[cite: 534]:
* [cite_start]**Bus Unit:** Tracks real-time GPS coordinates and transmits data via LoRa[cite: 71, 72].
* [cite_start]**Relay Unit:** Extends communication range by acting as a bridge between stops in zero-connectivity zones[cite: 52, 243].
* [cite_start]**Bus Stop Unit:** Receives LoRa packets, processes arrival data, and updates an LED Dot Matrix display[cite: 73, 534].

## 🚀 Key Technical Features
* [cite_start]**LoRa Communication:** Uses Chirp Spread Spectrum (CSS) to ensure long-range (5-7 km) rural coverage and high noise immunity[cite: 472, 489].
* [cite_start]**Independent ETA Prediction:** Bus stops independently calculate arrival times using stored waypoint archives and Haversine distance calculations, removing the need for internet dependency[cite: 143, 273].
* [cite_start]**Power Efficiency:** The system is designed for solar-powered deployment, with the MCU utilizing ultra-low power modes to conserve battery[cite: 463, 467].
* [cite_start]**Reliability:** Implements CRC (Cyclic Redundancy Check) for packet corruption detection and a 300-second heartbeat threshold for signal loss detection[cite: 367, 380].

## 🏗 Hardware Stack
| Component | Function | Protocol |
| :--- | :--- | :--- |
| **STM32L452RE** | Main Controller | N/A |
| **NEO-M8N** | GPS Position Tracking | UART |
| **SX1262** | LoRa Transceiver | SPI |
| **MAX7219** | LED Dot Matrix Display | SPI |

## 📐 Logic Flow
1. [cite_start]**Waypoint Generation:** The bus logs GPS coordinates every 2 seconds; a waypoint is generated every 500m using the Haversine formula[cite: 150, 166].
2. [cite_start]**Packet Transmission:** Bus broadcasts data packets containing `Bus ID`, `Bus Stop ID`, `Timestamp`, and `CRC`[cite: 279, 280].
3. [cite_start]**Stop Processing:** The bus stop validates the `Bus Stop ID` and checks if the bus is within the arrival zone (20m) to trigger status updates or calculate delays[cite: 292, 296].
4. [cite_start]**Downstream Propagation:** If a delay is detected, the village stop updates its schedule and propagates the delay to subsequent stops using the propagation rule: `scheduled arrival += delay`[cite: 313, 327].

## 📄 Documentation & Credits
* [cite_start]**Project Group:** Group 10 [cite: 3]
* [cite_start]**Mentorship:** WiSH Program, Texas Instruments [cite: 4, 5]
* [cite_start]**Key Algorithms:** Haversine Distance, Random Jitter (for collision avoidance)[cite: 199, 353].

---
[cite_start]*This project was developed to provide operational visibility and real-time transit information to over 800 million rural residents dependent on public transport[cite: 23, 24].*
