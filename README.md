# Temperature-Sensor Project

## Overview

This repository contains a set of Java-based projects for temperature and humidity monitoring, simulation, and remote control, primarily designed for use with the Raspberry Pi and the CrowPi platform. The system leverages the Pi4J library for GPIO interaction and includes integration with Microsoft Azure IoT for cloud connectivity.

The repository is organized into several subprojects:

- **pi4j-template**: Core applications and components for reading temperature and humidity from a DHT11 sensor, and controlling GPIO devices (e.g., LEDs, buttons).
- **ProjetoTempAzureIoT**: Application for sending temperature data to Microsoft Azure IoT Hub.
- **RemoteTempIoT**: Application for remotely controlling and monitoring temperature sensors.
- **SimulacaoIoT**: Simulation tools for IoT scenarios.

---

## Table of Contents

- [Features](#features)
- [Project Structure](#project-structure)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [How to Extend or Modify](#how-to-extend-or-modify)
- [Troubleshooting](#troubleshooting)
- [License](#license)

---

## Features

- Read temperature and humidity from a DHT11 sensor using the CrowPi platform.
- Control GPIO devices (LEDs, buttons) via Pi4J.
- Send sensor data to Microsoft Azure IoT Hub.
- Remotely monitor and control temperature sensors.
- Simulate IoT scenarios for testing and development.

---

## Project Structure

```
Temperature-Sensor/
│
├── pi4j-template/         # Core Pi4J applications and components
│   ├── src/
│   ├── pom.xml
│   └── ...
│
├── ProjetoTempAzureIoT/   # Azure IoT integration
│   ├── src/
│   ├── pom.xml
│   └── ...
│
├── RemoteTempIoT/         # Remote control and monitoring
│   ├── src/
│   ├── pom.xml
│   └── ...
│
├── SimulacaoIoT/          # IoT simulation tools
│   ├── src/
│   ├── pom.xml
│   └── ...
│
└── README.md              # Project documentation
```

---

## Requirements

- **Hardware:**
  - Raspberry Pi (recommended for physical sensor interaction)
  - CrowPi platform (for DHT11 sensor and GPIO)
  - DHT11 temperature and humidity sensor
  - Optional: LEDs, buttons, and other GPIO devices

- **Software:**
  - Java 11 or higher (Java 20 for some modules)
  - Maven 3.6+
  - Pi4J library (managed via Maven)
  - Microsoft Azure account (for IoT Hub integration)
  - Git

---

## Installation

### 1. Clone the Repository

```sh
git clone https://github.com/SaulDeAbreu/Temperature-Sensor.git
cd Temperature-Sensor
```

### 2. Build Each Subproject

Each subproject is a Maven project. You must build them individually:

```sh
cd pi4j-template
mvn clean install

cd ../ProjetoTempAzureIoT
mvn clean install

cd ../RemoteTempIoT
mvn clean install

cd ../SimulacaoIoT
mvn clean install
```

### 3. Hardware Setup

- Connect the DHT11 sensor to the appropriate GPIO pins on your Raspberry Pi.
- (Optional) Connect LEDs and buttons as described in the code comments.

#### Example: Wiring Diagram (ASCII Art)

```plaintext
+-----------------------------+
|        Raspberry Pi         |
|                             |
|   [5V]   o-----+            |
|                |            |
|   [GND]  o-----+-----+      |
|                      |      |
|   [GPIO24] o---+     |      |
|                |     |      |
|              [DHT11] |      |
|                |     |      |
|   [GPIO22] o---+     |      |
|                |     |      |
|               [LED]  |      |
|                |     |      |
|   [GND]  o-----+-----+      |
+-----------------------------+

DHT11 Sensor:
  - VCC  -> 5V (Pin 2)
  - GND  -> GND (Pin 6)
  - DATA -> GPIO24 (Pin 18)

LED:
  - Anode (+) -> GPIO22 (Pin 15) (with 220Ω resistor)
  - Cathode (-) -> GND (Pin 6)
```

---

## Usage

### 1. Running the Pi4J Applications

#### Example: Reading Temperature and Humidity

```sh
cd pi4j-template
mvn exec:java -Dexec.mainClass="pt.tpsi.ad.pi4j.aplications.HumiTempApp"
```

This will print the current temperature and humidity readings from the DHT11 sensor.

#### Example: Button and LED Control

```sh
cd pi4j-template
mvn exec:java -Dexec.mainClass="pt.tpsi.ad.pi4j.ButtonLedApp"
```

This application toggles an LED and counts button presses.

---

### 2. Sending Data to Azure IoT Hub

1. Configure your Azure IoT Hub credentials in the `ProjetoTempAzureIoT` source code or via environment variables.
2. Run the application:

```sh
cd ProjetoTempAzureIoT
mvn exec:java -Dexec.mainClass="org.example.ConsoleProjectTemp"
```

---

### 3. Remote Monitoring and Control

```sh
cd RemoteTempIoT
mvn exec:java -Dexec.mainClass="org.example.RemoteControlTemp"
```

---

### 4. Simulating IoT Scenarios

```sh
cd SimulacaoIoT
mvn exec:java -Dexec.mainClass="org.example.SendMessage"
```

---

## How to Extend or Modify

### Adding New Sensors or Components

- Implement new components in `pi4j-template/src/main/java/pt/tpsi/ad/pi4j/components/`.
- Follow the structure of `HumiTempComponent.java` for reading sensor data.

### Creating New Applications

- Implement the `Application` interface in `pi4j-template/src/main/java/pt/tpsi/ad/pi4j/`.
- Use the Pi4J context for GPIO operations.

### Integrating with Other Cloud Services

- Add dependencies in the relevant `pom.xml`.
- Implement new modules following the pattern in `ProjetoTempAzureIoT`.

---

## Troubleshooting

- **Permission Issues:** Ensure your user has permission to access GPIO and device files. Run with `sudo` if necessary.
- **DHT11 Not Detected:** Check wiring and that the Linux driver for DHT11 is installed and exposes the correct files.
- **Azure IoT Connection Fails:** Verify your IoT Hub credentials and network connectivity.
- **Build Errors:** Ensure you are using the correct Java version for each module.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Contact

For questions or contributions, please open an issue or pull request on GitHub. 