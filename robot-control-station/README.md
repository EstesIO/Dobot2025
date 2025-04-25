# 🤖 Robot Control Station - ESP32 + ESPHome + MQTT

This project sets up a robot control station using an **ESP32 microcontroller**, **ESPHome**, and **MQTT**, with Node-RED or Home Assistant integration.

## 🧰 Hardware Used

| Component             | Description                                       |
|----------------------|---------------------------------------------------|
| ESP32 Dev Board      | Main microcontroller                              |
| 24V Power Supply     | Input voltage for system                          |
| Buck Converter       | 24V → 5V for powering the ESP32                   |
| Relay Module (4CH)   | Controls Light Tree outputs, 1 spare channel      |
| Light Tree           | Visual indicators: Green (Run), Red (Stop), Yellow (Manual) |
| Push Buttons         | Green (Start), Red (Stop), Yellow (Human), E-Stop (NC) |

## 🧠 Platform: ESPHome + MQTT

This system uses **ESPHome** to publish and subscribe to MQTT topics. ESPHome is highly compatible with Home Assistant and Node-RED.

### MQTT Topic Map

| Action           | MQTT Topic             | Payload       |
|------------------|-------------------------|---------------|
| Start            | `robot/start`           | `pressed`     |
| Stop             | `robot/stop`            | `pressed`     |
| Manual Override  | `robot/manual`          | `pressed`     |
| Emergency Stop   | `robot/estop`           | `triggered`   |
| Light Control    | `robot/light/<color>`   | `ON` / `OFF`  |

## 🔌 Wiring Overview

### 🔧 GPIO Wiring

| GPIO | Function            | Notes                      |
|------|---------------------|----------------------------|
| 16   | Green Start Button  | INPUT_PULLUP               |
| 17   | Red Stop Button     | INPUT_PULLUP               |
| 18   | E-Stop (NC)         | INPUT_PULLUP               |
| 19   | Human Mode Button   | INPUT_PULLUP               |
| 25   | Green Light Output  | Relay Channel 1 (IN1)      |
| 26   | Red Light Output    | Relay Channel 2 (IN2)      |
| 27   | Yellow Light Output | Relay Channel 3 (IN3)      |
| —    | Spare               | Relay Channel 4 (IN4)      |

### 🔋 Power Wiring

- 24V Power Supply:
  - + → Buck Converter VIN & Relay VCC
  - – → GND (shared with ESP32 and relay GND)

- Buck Converter:
  - Output +5V → ESP32 VIN
  - Output GND → ESP32 GND

### 🔁 Relay Output Wiring

| Relay Channel | Light Color | Connected Pins                         |
|---------------|-------------|----------------------------------------|
| 1 (IN1)       | Green       | COM → 24V+, NO → Green light V+        |
| 2 (IN2)       | Red         | COM → 24V+, NO → Red light V+          |
| 3 (IN3)       | Yellow      | COM → 24V+, NO → Yellow light V+       |
| 4 (IN4)       | — (Spare)   | Available for future use               |

All light grounds connect back to the 24V GND rail.

## 📷 Wiring Diagram
![Wiring Diagram](images/diagram.png)

## 📋 Setup Steps

1. Flash the ESP32 with `esphome.yaml` using ESPHome
2. Wire buttons and lights as described above
3. Set up Mosquitto MQTT broker on Windows PC or use Home Assistant
4. Create Node-RED flows that subscribe to relevant MQTT topics
5. Use MQTT to control robot state and signal lights

## 🔐 Security Note
Ensure your MQTT broker is password-protected or isolated in a secure network segment.

---

### 📂 Files Included in this Repo
- `esphome.yaml`: ESPHome YAML config for buttons, lights, and MQTT
- `images/diagram.png`: Wiring diagram
- `flows/robot_control_flow.json`: Node-RED flow export (optional)

### 🧠 Next Steps
- Add `esphome.yaml`
- Add Node-RED flow for Windows-based robot control

Stay tuned for the full repo rollout!
