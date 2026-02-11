🛰️ AstroVital: Deep Space Telemetry Bridge

AstroVital is a full-stack biomedical telemetry system designed to simulate the monitoring of astronaut vital signs during Extravehicular Activities (EVAs). It bridges the gap between embedded hardware (Space Suit) and mission control software using IoT protocols optimized for high-latency environments.

📖 Project Overview

In deep space missions, real-time physiological monitoring is critical. This project simulates a Class III Medical Device data pipeline. It generates synthetic physiological waveforms (ECG, SpO2) at the edge (firmware), packetizes them, and transmits them via MQTT to a ground station dashboard for anomaly detection.

Key Features

Real-time ECG Synthesis: Uses a mathematical model to generate PQRST waveforms in C++ (simulating an AD8232 sensor).

Hypoxia Detection Algorithm: Monitors SpO2 saturation and triggers "CRITICAL" alerts if levels drop below 90%.

Low-Overhead Protocol: Uses MQTT (Message Queuing Telemetry Transport) to minimize bandwidth usage, simulating deep-space link constraints.

Mission Control Dashboard: A Python-based visualization tool (Streamlit) that renders live heart rates and system status.

🏗️ System Architecture

The system is composed of three decoupled layers:

graph LR
    A[Edge Device / C++] -- JSON Telemetry --> B(MQTT Broker);
    B -- Subscribe --> C[Mission Control / Python];
    C -- Alert Logic --> D((User Interface));


The Space Suit (Firmware): Runs on ESP32/Arduino. It acts as the sensor interface, sampling data at 20Hz and acting as an MQTT Publisher.

The Comms Relay (Broker): A central MQTT broker (Mosquitto) that decouples the sender from the receiver, allowing for asynchronous communication.

Mission Control (Software): A Python application that subscribes to the telemetry topic, buffers the data, and visualizes it in real-time.

🛠️ Tech Stack

Firmware (Edge)

Language: C++ (Arduino Framework)

Hardware: ESP32 Dev Kit V1 (Simulated)

Libraries: ArduinoJson (Serialization), PubSubClient (Connectivity)

Software (Ground Station)

Language: Python 3.10+

Framework: Streamlit (Web Dashboard)

Data Handling: Pandas (Time-series buffer), Paho-MQTT (Client)

🚀 Installation & Setup

1. Clone the Repository

git clone [https://github.com/YOUR_USERNAME/AstroVital.git](https://github.com/YOUR_USERNAME/AstroVital.git)
cd AstroVital


2. Setup Python Environment (Ground Station)

It is recommended to use a virtual environment.

pip install -r requirements.txt


3. Run the Simulation

Option A: Full Simulation (No Hardware)
Open two terminal windows.

Terminal 1 (Dashboard): streamlit run mission_control/dashboard.py

Terminal 2 (Data Generator): python simulation/data_generator.py

Option B: Hardware Mode (ESP32)

Open firmware/main.cpp in Arduino IDE.

Install libraries: PubSubClient and ArduinoJson.

Update ssid and password with your WiFi credentials.

Flash to ESP32.

🧬 Biomedical Engineering Concepts

This project demonstrates competency in:

Signal Processing: Generating and filtering biological signals.

Interoperability: Sending medical data between C++ hardware and Python software.

Safety-Critical Logic: Implementing thresholds for life-threatening conditions (Hypoxia).

🔮 Future Roadmap

[ ] Implement Heart Rate Variability (HRV) analysis.

[ ] Add database storage (SQLite) for post-mission analysis.

[ ] Secure the MQTT connection with TLS/SSL.

📄 License

Distributed under the MIT License. See LICENSE for more information.
