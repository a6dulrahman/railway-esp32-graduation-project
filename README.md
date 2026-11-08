# Railway Traffic Signal and Train Control System

A railway control prototype built using two ESP32 boards and MicroPython. The system provides a web-based interface for controlling six railway traffic signals and wirelessly manages train motor speed through ESP-NOW communication.

## Project Overview

The project consists of two ESP32 units:

- **Signal Controller:** Hosts a web interface over Wi-Fi Access Point mode and controls six traffic signals.
- **Train Controller:** Receives wireless commands through ESP-NOW and controls the train motor speed using PWM.

Users can interact with the traffic signals through a browser. Each signal selection triggers a corresponding command to control the train.

## Features

- Web-based control interface accessible through a browser.
- Control of six traffic signals (T1–T6).
- Three signal states: Red, Yellow, and Green.
- Wireless communication between ESP32 boards using ESP-NOW.
- Train motor speed control using PWM.
- Three motor states: Stop, Medium, and Fast.
- Automatic motor stop if no new command is received for five seconds.

## Hardware and Technologies

- ESP32 microcontrollers (2 boards)
- MicroPython
- Python
- HTML
- CSS
- JavaScript
- Wi-Fi Access Point
- ESP-NOW wireless communication
- PWM motor control
- Motor driver

## System Architecture

### 1. Signal Controller (`src/main.py`)

The first ESP32:

1. Initializes ESP-NOW communication.
2. Configures the GPIO pins for six traffic signals.
3. Creates a Wi-Fi Access Point.
4. Hosts an HTTP server on port 80.
5. Serves a web interface for controlling the signals.
6. Sends train commands according to the selected signal:

| Signal State | Train Command |
|---|---|
| Red | STOP |
| Yellow | MEDIUM |
| Green | FAST |
| Off | STOP |

### 2. Train Controller (`src/motor/main.py`)

The second ESP32:

1. Initializes the motor driver pins.
2. Configures PWM at 1 kHz.
3. Establishes ESP-NOW communication.
4. Receives commands from the signal controller.
5. Adjusts motor speed according to the received command.
6. Stops the motor if no new command is received within five seconds.

## Project Structure

```text
railway-esp32-graduation-project/
│
├── config
│
├── src/
│   ├── main.py
│   │
│   └── motor/
│       └── main.py
│
└── README.md
```

## Setup and Usage

### Requirements

- Two ESP32 development boards.
- MicroPython firmware installed on both boards.
- A compatible motor driver and DC motor.
- A browser-enabled device.

### Configuration

1. Configure the train ESP32 MAC address in the signal controller code.
2. Ensure both ESP32 boards use the same Wi-Fi channel for ESP-NOW communication.
3. Verify the GPIO pin connections according to the hardware setup.
4. Configure the Wi-Fi Access Point credentials before deployment.

### Running the Project

1. Upload `src/motor/main.py` to the train controller ESP32.
2. Upload `src/main.py` to the signal controller ESP32.
3. Power on both boards.
4. Connect a computer or mobile device to the ESP32 Wi-Fi Access Point.
5. Open the ESP32 IP address in a web browser.
6. Select a traffic signal to control the corresponding train movement command.

## Safety Notice

This project is an educational prototype, not a certified railway signaling or train-control system. It should not be used in real railway operations. A production system would require independent safety mechanisms, hardware-level fail-safes, and extensive testing.

## Author

Abdulrahman

GitHub Repository: https://github.com/a6dulrahman/railway-esp32-graduation-project
