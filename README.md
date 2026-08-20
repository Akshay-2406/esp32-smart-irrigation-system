# 🌾 Adaptive Multi-Sensor Predictive Smart Irrigation System

An IoT-enabled smart irrigation system powered by the **ESP32 microcontroller**. Unlike traditional threshold systems, this project utilizes multi-sensor predictive modeling—combining soil moisture, ambient temperature, and relative humidity—to calculate an **Adaptive Dryness Index (DI)**.

![Hardware Prototype](images/prototype.jpg)

---

## 🔥 Key Features

* **Multi-Sensor Fusion:** Reads real-time data from Capacitive Soil Moisture, DS18B20 Temperature, and DHT Sensors.
* **Predictive Control Logic:** Uses a dynamic Dryness Index (DI) formula considering temperature shifts and humidity parameters to trigger irrigation[cite: 1].
* **Crop-Specific Optimization:** Validated across 5 crop profiles (*Paddy, Sugarcane, Groundnut, Ragi, Mango*) with custom moisture and heat risk thresholds[cite: 1].
* **Dual Monitoring:** Local real-time readout on a 16x2 I2C LCD paired with remote cloud telemetry[cite: 1].
* **Water Conservation:** Stops irrigation automatically at optimal saturation to prevent deep percolation and resource waste[cite: 1].

---

## 📐 Mathematical Model (Dryness Index)

Irrigation decisions are made dynamically using the following equation[cite: 1]:

$$DI = (100 - M) + k_{\text{temp}} \cdot (T - 25) - k_{\text{hum}} \cdot (H)$$

Where:
* $M$ = Soil Moisture Percentage (%)[cite: 1]
* $T$ = Soil/Ambient Temperature (°C)[cite: 1]
* $H$ = Relative Humidity (%)[cite: 1]
* $k_{\text{temp}}, k_{\text{hum}}$ = Environmental weighting factors[cite: 1]

*Condition:* If **$DI > \text{Threshold}$**, the relay activates the water pump[cite: 1].

---

## 🛠️ System Architecture & Stack

* **Microcontroller:** ESP32 Dev Kit[cite: 1]
* **Languages:** Embedded C / C++[cite: 1]
* **Software Tools:** Arduino IDE, ThingSpeak Cloud Platform[cite: 1]
* **Hardware Modules:** 5V Relay, Mini Water Pump, 16x2 I2C LCD[cite: 1]

---

## 📁 Repository Structure

```text
├── docs/            # Research report & system flowcharts[cite: 1]
├── firmware/        # ESP32 C++ source code & library imports[cite: 1]
├── hardware/        # Pin mapping tables, BOM, and circuit layout[cite: 1]
├── images/          # Hardware photos & system performance graphs[cite: 1]
└── simulation/      # Wokwi simulation logs & multi-crop evaluation[cite: 1]
