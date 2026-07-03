# Rural Bus Tracking and Passenger Information System

An off-grid, low-power, and scalable transit intelligence solution designed to provide real-time bus arrival information in rural areas without the need for cellular networks or internet connectivity.

## 🔧 System Architecture
The system employs a distributed architecture utilizing three specialized hardware units:
* **Bus Unit:** Tracks real-time GPS coordinates and transmits data via LoRa.
* **Relay Unit:** Extends communication range by acting as a bridge between stops in zero-connectivity zones.
* **Bus Stop Unit:** Receives LoRa packets, processes arrival data, and updates an LED Dot Matrix display.

## 🚀 Key Technical Features
* **LoRa Communication:** Uses Chirp Spread Spectrum (CSS) to ensure long-range (5-7 km) rural coverage and high noise immunity.
* **Independent ETA Prediction:** Bus stops independently calculate arrival times using stored waypoint archives and Haversine distance calculations, removing the need for internet dependency.
* **Power Efficiency:** The system is designed for solar-powered deployment, with the MCU utilizing ultra-low power modes to conserve battery.
* **Reliability:** Implements CRC (Cyclic Redundancy Check) for packet corruption detection and a 300-second heartbeat threshold for signal loss detection.

## 🏗 Hardware Stack
| Component | Function | Protocol |
| :--- | :--- | :--- |
| **STM32L452RE** | Main Controller | N/A |
| **NEO-M8N** | GPS Position Tracking | UART |
| **SX1262** | LoRa Transceiver | SPI |
| **MAX7219** | LED Dot Matrix Display | SPI |

## 📐 Logic Flow
1. **Waypoint Generation:** The bus logs GPS coordinates every 2 seconds; a waypoint is generated every 500m using the Haversine formula.
2. **Packet Transmission:** Bus broadcasts data packets containing `Bus ID`, `Bus Stop ID`, `Timestamp`, and `CRC`.
3. **Stop Processing:** The bus stop validates the `Bus Stop ID` and checks if the bus is within the arrival zone (20m) to trigger status updates or calculate delays.
4. **Downstream Propagation:** If a delay is detected, the village stop updates its schedule and propagates the delay to subsequent stops using the propagation rule: `scheduled arrival += delay`.

## 📄 Documentation & Credits
* **Project Group:** Group 10
* **Mentorship:** WiSH Program, Texas Instruments
* **Key Algorithms:** Haversine Distance, Random Jitter (for collision avoidance).

---
*This project was developed to provide operational visibility and real-time transit information to over 800 million rural residents dependent on public transport.*
