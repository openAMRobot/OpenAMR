# Bill of Materials (BOM) repository

## Overview

This document provides a comprehensive list of all assemblies and their corresponding files in the BOM repository. It also includes details on sheet metal parts, fasteners, technological operations, and origin components.

## Sheet metal parts

Sheet metal parts are subject to production variations. The current designs are based on the following coefficients and radii:

- **Coefficient (K):** 0.47
- **Sheet metal specifications:**
  - **0.8 mm Sheet:** Radius (R) = 1.2
  - **1.2 mm Sheet:** Radius (R) = 1.5
  - **2.0 mm Sheet:** Radius (R) = 2.4

### Post-production

- Parts may be painted after bending.
- Riveting nuts can be installed before painting if the threaded part is protected from the coating.
- Screws installed without lock washers should be secured with a thread lock (e.g., Loxeal 55-03).

**Note:** All components are highly interconnected and their functionality is dependent on one another.

## MMP - Multipurpose Mobile Platforms

### List of fasteners and quantities

Detailed information on fasteners and their quantities used in assemblies is listed in the corresponding sections.

### Technological operations

Each assembly comes with a list of required technological operations. Ensure that all operations are followed as specified.

## Origin components

The following components are used in the assemblies:

- **Heavy duty drive wheel:** Blickle GEVN 200/30H7
- **Light duty swivel castor:** Blickle LPA-VSTH 35K
- **Oval flange bearing units:**
  - REXNORD UCFL 205 C 655472 (d25)
  - REXNORD UCFL 206 C 666412 (d30)
- **Rivet nuts:**
  - M4 Blind Rivet Nut - Round Thin - Stainless Steel
  - M5 Blind Rivet Nut - Round Thin - Stainless Steel
  - M6 Blind Rivet Nut - Round Thin - Stainless Steel
  - M8 Blind Rivet Nut - Round Thin - Stainless Steel
- **Feather keys:**
  - 4x4x25 DIN 6885-UNI 6604 (formerly ISO 773)
  - 8x7x28 DIN 6885-UNI 6604 (formerly ISO 773)
- **Screwed spacer sleeve:** TFF-M3/25 FIX&FASTEN
- **BLDC Motor:** Z4BLD60-24GN-30S/4GN 25K 
- **Laser range scanner:** RPLIDAR A1-A1M8
- **Camera module:** NVision Assem
- **Proximity sensor:** E18-D80NK
- **US sensor:** JSN-SR04T
- **LED module:** 3 LED RGB Module 0.72W SWP

__________________________________________________________

# OpenAMR – Preliminary Electronics Bill of Materials (BOM)

## Overview

This Bill of Materials preliminary defines the electronics used in the OpenAMR development platform.  
The system follows a two-layer architecture:

- **High-level control**: Raspberry Pi 5 (ROS2, navigation, perception, UI)  
- **Real-time control**: Teensy 4.0 (motor control, encoders, IMU)  

The setup is designed for differential drive mobile robot development and software validation.

---

## Core Computing

| Item | Model | Qty | Description |
|------|------|-----|------------|
| Main Computer | Raspberry Pi 5 (8GB) | 1 | High-level controller running ROS2, SLAM, navigation, and UI |
| Microcontroller | Teensy 4.0 | 1 | Real-time controller for motors, sensors, and low-level logic |
| Communication | USB cable (USB-A ↔ Micro USB / USB-C) | 1 | Serial communication between Raspberry Pi and Teensy |

---

## Drive System

| Item | Model | Qty | Description |
|------|------|-----|------------|
| BLDC Motor | ZDBLD60-24GN-30S | 2 | 24V BLDC motor for differential drive |
| Gearbox | 4GN 25K | 2 | Gear reduction for torque increase |
| Motor Driver | ZBLD-C20-120L2R | 2 | BLDC motor driver (PWM speed control, digital direction control) |

---

## Feedback Sensors

| Item | Model | Qty | Description |
|------|------|-----|------------|
| Magnetic Encoder | AS5040 | 2 | Wheel position sensing for odometry (Quadrature (A/B) or SPI interface) |
| IMU | MPU6050 | 1 | 6-axis inertial measurement unit (accelerometer + gyroscope, I2C) |

---

## Perception Sensors

| Item | Model | Qty | Description |
|------|------|-----|------------|
| LiDAR | RPLIDAR A1 | 1 | 2D laser scanner for SLAM and obstacle detection (USB) |
| Camera | Raspberry Pi Camera Module / Arducam IMX219 | 1 | Vision sensor for docking and computer vision tasks (CSI interface) |

---

## Power System

| Item | Model | Qty | Description |
|------|------|-----|------------|
| Battery | 24V Li-ion / LiFePO4 pack | 1 | Main power source for motors and electronics |
| DC-DC Converter | LM2596 Buck Converter (24V → 5V, ≥5A) | 1 | Power supply for Raspberry Pi |
| DC-DC Converter | DROK 24V → 5V/12V Step-Down Module | 1 | Power supply for sensors and auxiliary electronics |
| Protection | Inline fuse (rated above motor current) | 1 | Overcurrent protection on main power line |
| Safety | Emergency stop switch | 1 | Manual power cutoff for safety |

---

## Interfaces and Integration

| Item | Model | Qty | Description |
|------|------|-----|------------|
| Prototyping Board | Breadboard / Perfboard | 1 | Temporary wiring platform (used until custom PCB is developed) |
| Power Distribution | Terminal blocks / distribution bus | 1 set | Power routing for 24V and low-voltage lines |
| Wiring | Motor cables, signal wires, connectors | 1 set | Electrical connections between components |

---

## Alternative Drive Option (ZL Tech)

| Item | Model | Qty | Description |
|------|------|-----|------------|
| Hub Motor | ZLLG80ASM250-L | 2 | Integrated BLDC motor with built-in encoder |
| Driver | ZLAC8015D | 1–2 | Motor controller with RS485/CAN interface |

---

## System Interfaces Summary

- Raspberry Pi ↔ Teensy: USB Serial  
- Teensy ↔ Motor Drivers: PWM (speed) + Digital IO (direction)  
- Teensy ↔ Encoders: Quadrature (A/B) or SPI interface  
- Teensy ↔ IMU: I2C  
- Raspberry Pi ↔ LiDAR: USB  
- Raspberry Pi ↔ Camera: CSI  

---

## Notes

- The system is designed for modular expansion and hardware replacement.  
- Breadboard or perfboard is used for initial prototyping before designing a custom carrier PCB.  
- All components are selected to support ROS2-based mobile robotics development.  

[![Support on Patreon - Supporter Tier – €5/month](https://img.shields.io/badge/Support%20on-Patreon-orange)](https://www.patreon.com/cw/Botshare)
[![Donate via PayPal](https://img.shields.io/badge/Donate-PayPal-blue.svg)](https://www.paypal.com/paypalme/BotshareAI)
[![Donate on GitHub](https://img.shields.io/badge/Sponsor%20on-GitHub-pink?logo=github-sponsors)](https://github.com/sponsors/openAMRobot)
