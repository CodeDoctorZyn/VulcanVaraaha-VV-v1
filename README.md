# VulcanVaraaha-VV-v1
VV-v1 is a cost-effective, AI-powered autonomous drone system designed for real-time object detection, tracking, and surveillance. Built during my undergraduate studies, this project integrates embedded systems, computer vision, and IoT technologies to create a versatile drone platform capable of autonomous operations without reliance on expensive hardware.
The system uses an ESP32-CAM module for real-time video capture, NodeMCU (ESP8266) for sensor data processing, and OpenCV-based AI algorithms for object detection—all while streaming data to the cloud via ThingSpeak for remote monitoring.

## Key Features
Autonomous Object Detection – Real-time identification and tracking of objects using OpenCV and deep learning models

Dual-Processor Architecture – ESP32-CAM handles video processing; ESP8266 manages sensors and communication

Live Video Streaming – Accessible via local IP for low/high-resolution feeds

Environmental Monitoring – Temperature, humidity (DHT11), and motion detection (PIR sensor)

GPS Integration – NEO-6M module for real-time location tracking and waypoint navigation

Cloud Connectivity – ThingSpeak integration for live data visualization and storage

Cost-Effective Design – 3D-printed PLA frame reduces weight and production costs

User-Friendly Interface – Web-based monitoring and control

## Motivation 

As someone with a pure software background during my undergraduate studies, this project felt like venturing into no-man's land. Every conversation—whether with peers or mentors—revealed the same concerns: tight timelines, limited resources, and my own skill gaps at the
time.
Building a drone from scratch meant stepping far outside my comfort zone. I had to wrestle with:
Hardware I didn't understand – Soldering components, debugging circuit boards, and praying the magic smoke wouldn't escape
Embedded systems I'd never touched – Writing C++ for microcontrollers when Python was my safe space
Physics I hadn't considered – Weight distribution, thrust-to-weight ratios, aerodynamics—concepts that don't exist in a code editor
Failures I couldn't debug with a print statement – When the drone wouldn't lift off, there was no console log to check

This project represents my curiosity-driven approach to solving real-world problems:

How can we make drone technology accessible? → By building a cost-effective alternative to expensive commercial drones

How do autonomous systems make decisions? → By implementing AI algorithms on embedded hardware

How can data be useful in real-time? → By integrating cloud platforms for live monitoring


## System Architecture

┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│                 │     │                  │     │                 │
│   ESP32-CAM     │────▶│   Object Detection│────▶│   Live Video    │
│   (Camera)      │     │   (OpenCV/AI)     │     │   Streaming     │
│                 │     │                  │     │                 │
└─────────────────┘     └──────────────────┘     └─────────────────┘
         │                          │                         │
         │                          │                         │
         ▼                          ▼                         ▼
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│                 │     │                  │     │                 │
│   ESP8266       │────▶│   DHT11/PIR/GPS  │────▶│   ThingSpeak    │
│   (NodeMCU)     │     │   Sensors        │     │   Cloud         │
│                 │     │                  │     │                 │
└─────────────────┘     └──────────────────┘     └─────────────────┘

## Hardware Components
| Component | Specification | Purpose |
|-----------|---------------|---------|
| **Flight Controller** | Custom-built | Drone stabilization & control |
| **ESP32-CAM** | OV2640 camera, WiFi/BT | Video capture & streaming |
| **NodeMCU (ESP8266)** | 80MHz CPU, WiFi | Sensor data processing |
| **GPS Module** | NEO-6M | Location tracking |
| **DHT11 Sensor** | Temperature/Humidity | Environmental monitoring |
| **PIR Sensor** | Motion detection | Intrusion detection |
| **Frame** | 3D-printed PLA | Lightweight, durable body |
| **Motors** | Brushless (outrunner) | Efficient propulsion |
| **ESCs** | Electronic Speed Controllers | Motor speed regulation |
| **Battery** | LiPo | Power source |

## Software Stack

### Languages & Frameworks
Python 3.8+ – AI/ML algorithms, OpenCV integration

C++ (Arduino) – Embedded firmware for ESP32/ESP8266

OpenCV – Computer vision & object detection

TensorFlow/PyTorch – Deep learning models (implementation-ready)

### Development Tools
Arduino IDE – Microcontroller programming

VS Code – Code development & debugging

ThingSpeak – IoT cloud platform for data visualization

### Key Libraries
#### Python Dependencies

opencv-python==4.5.5   # Computer vision

numpy==1.21.0          # Numerical operations

pyserial==3.5          # Serial communication

requests==2.26.0       # HTTP requests

## Getting Started
### Prerequisites
Arduino IDE with ESP32/ESP8266 board support

Python 3.8+ with pip

Basic electronics knowledge (soldering, wiring)

### Hardware Setup
Assemble the drone frame (3D-printed PLA parts)

Mount the components:

ESP32-CAM for vision

NodeMCU with sensors (DHT11, PIR, GPS)

Flight controller with ESCs and motors

Wire the connections (refer to pinout diagram below)

Power up with LiPo battery

## Software Installation

# Clone the repository
git clone https://github.com/cod3doctorzyn/VulcanVaraaha-VV-v1.git

cd VulcanVaraaha-VV-v1.git

## Install Python dependencies
pip install -r requirements.txt

## Configuration
1. WiFi Settings – Update SSID and password in both firmware files:

const char* WIFI_SSID = "YOUR_NETWORK";

const char* WIFI_PASS = "YOUR_PASSWORD";

3. ThingSpeak – Create a channel and update API key:
   
const char* apiKey = "YOUR_API_KEY";

const unsigned long channelID = YOUR_CHANNEL_ID;


## Usage
1. Power On the System
Connect the LiPo battery

Wait for LED indicators to stabilize

2. Access Live Video Feed
Find ESP32-CAM IP address from Serial Monitor

Open browser and navigate to:

http://[ESP32-IP]/cam-lo.jpg (low resolution)

http://[ESP32-IP]/cam-hi.jpg (high resolution)

3. Monitor Sensor Data
Visit your ThingSpeak channel

View real-time temperature, humidity, and motion data

4. Object Detection
Run the Python script for AI processing:

bash
python object_detection.py --source http://[ESP32-IP]/cam-hi.jpg


## Security Considerations
Encrypted communication between drone and ground station

Secure boot mechanisms for firmware integrity

Access control & authentication

Regular firmware updates

Physical tamper detection

## Future Enhancements

Automated environmental mapping – Add LiDAR for 3D mapping

Video database – Store and analyze historical footage

Improved battery – Higher capacity for extended flight time

Web analytics – Track user behavior and system performance

Disaster recovery – Automated failsafe protocols

Swarm capabilities – Multiple drone coordination

## Lessons Learned

This project taught me:

End-to-end system design – From hardware assembly to software integration

Embedded AI optimization – Running computer vision on resource-constrained devices

IoT cloud integration – Real-time data streaming and visualization

Problem-solving under constraints – Balancing cost, performance, and functionality

Documentation importance – Clear technical communication for reproducibility


## About Me
I'm a about to be a graduate (DEC 2026) passionate about:

Cybersecurity Practises - Threat analysis and Offesive secuitrity practises

Embedded Systems – Bridging hardware and software

Computer Vision – Teaching machines to see and understand

IoT & Cloud – Connecting devices for intelligent decision-making

Autonomous Systems – Building things that think for themselves

This project represents my curiosity-driven approach to technology—not just using existing solutions, but understanding how they work and building better, more accessible alternatives.

## License
This project is open-source under the MIT License. Feel free to use, modify, and distribute with attribution.

## Acknowledgments
My undergraduate supervisors and peers for guidance

Open-source communities (OpenCV, Arduino, ESP32)

Jay Lord – For the motivation to properly document my work

⭐ If you find this project interesting, consider giving it a star!



Help with the commit messages or GitHub setup?



