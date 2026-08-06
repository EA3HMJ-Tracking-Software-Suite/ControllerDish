# ControllerDish

ControllerDish is the embedded hardware and firmware responsible for moving and monitoring a two-axis antenna system. It controls the azimuth and elevation motors, reads the corresponding position sensors, applies movement and safety limits, and communicates with [DriverDish](https://github.com/EA3HMJ-Tracking-Software-Suite/DriverDish).

![ControllerDish](https://github.com/EA3HMJ-Tracking-Software-Suite/ControllerDish/assets/2368602/59209ca7-eb7c-49db-aca0-ce0e430feea9)

## Control features

- Independent closed-loop control of the azimuth and elevation axes.
- Continuous position feedback from absolute encoders and inclinometers using Modbus RTU at 115200 bps.
- Separate outputs for azimuth and elevation motor drivers.
- Communication with DriverDish over RS-485; hardware 2.3 can alternatively use Ethernet and Modbus TCP.
- Configurable motion range and pointing limits.
- Controlled acceleration, speed, approach, and stopping of both axes.
- Continuous controller, position, movement, and communication status reporting.
- Safety stop control and support for hardware limit switches on compatible versions.
- Emergency stow input on supported hardware, allowing the antenna to move to a predefined safe position.
- Motor current monitoring on supported DC-motor versions.
- Support for 5 V and 12 V position sensors.

## Important requirement for hardware 2.x

> [!IMPORTANT]
> ControllerDish hardware **2.x requires an ESP32-S3 DevKitC fitted with an ESP32-S3-N16R8 module**. The N16R8 memory configuration is an essential hardware requirement; do not substitute it with a lower-memory or different ESP32-S3 variant.

Hardware 2.x uses firmware built specifically for the ESP32-S3 platform and is not a drop-in firmware replacement for the ESP32 hardware used by other ControllerDish board families.

## Recommended hardware for new projects

> [!TIP]
> Use **ControllerDish hardware 2.3** for all new projects. It is the current recommended design and supports both RS-485/Modbus RTU and Ethernet/Modbus TCP communication.

For installations that use AC motors and variable-frequency drives, use hardware 2.x together with the dedicated ControllerDish VFD interface module.

## Hardware version comparison

The hardware families are alternatives designed for different power and motor-control requirements. A higher family number does not necessarily replace every earlier design.

| Hardware | Status and purpose | Motor control | Power | Safety, sensing, and communication |
| --- | --- | --- | --- | --- |
| **1.0-1.3** | Obsolete early designs | DC motors | Version-dependent | Superseded by later 1.x boards |
| **1.4** | Active DC-motor design | Previous driver or XY-160D; supports the XY-160D motor brake | 12 V input with onboard 24 V step-up converter | RS-485 communication, position sensors, remote controller, and automatic motor-driver detection in compatible firmware |
| **1.5** | Active flexible DC-motor design | Two IBT-2 H-bridge drivers; each motor can use a separate supply and is monitored independently | Direct 12 V or 24 V input; no onboard voltage step-up | RS-485, position sensors, motor-current monitoring, and auxiliary controller bus |
| **2.0** | ESP32-S3 DC-motor platform | Two IBT-2 H-bridge drivers | 12 V or 24 V; motors may use different supply voltages | Requires **ESP32-S3-N16R8**; four mechanical or electronic limit-switch inputs and improved motor current/voltage monitoring |
| **2.1** | Evolution of 2.0 | Same as 2.0 | Same as 2.0 | Adds an emergency stow input |
| **2.2** | Environmental monitoring version | Same as 2.1 | Same as 2.1 | Adds onboard temperature, humidity, and pressure monitoring through an AHT20/BME280 module; includes auxiliary Modbus RTU connection |
| **2.3** | Network-enabled 2.x version | Same as 2.2 | Same as 2.2 | Selectable RS-485/Modbus RTU or W5500 Ethernet/Modbus TCP connection; removes the auxiliary RS-485 module |
| **3.x** | **Discontinued** | Former integrated VFD-control design | - | Replaced by hardware 2.x used with the dedicated ControllerDish VFD interface module; not recommended for new projects |

## Version 2.x capabilities

The 2.x family is the current ESP32-S3-based DC-motor controller platform. Depending on the board revision, it provides:

- 12 V or 24 V DC controller supply.
- Independent supply voltage for each DC motor.
- Two IBT-2 H-bridge motor drivers.
- Four opto-isolated limit-switch inputs: minimum and maximum for each axis.
- Independent current and voltage monitoring for both motors.
- Absolute azimuth and elevation sensors over Modbus RTU.
- Emergency stow input from version 2.1 onward.
- Temperature, pressure, and humidity monitoring from version 2.2 onward.
- RS-485/Modbus RTU or Ethernet/Modbus TCP host communication on version 2.3.

## Firmware compatibility

> [!WARNING]
> Hardware 1.x and 2.x use different firmware builds. The firmware packages are **not interchangeable**. Always select the package that matches the ControllerDish hardware family and its ESP32 module.

The latest release provides two separate firmware packages:

| Firmware package | ControllerDish hardware | Required ESP32 module |
| --- | --- | --- |
| `ControllerDishModBusTCP_Hv1_Update_v4.1.zip` | Hardware **1.x** | **ESP32-DEVKITC-32D** |
| `ControllerDishModBusTCP_Hv2_Update_v4.1.zip` | Hardware **2.x** | **ESP32-S3 DevKitC with ESP32-S3-N16R8** |

Download the appropriate package from the [latest ControllerDish release](https://github.com/EA3HMJ-Tracking-Software-Suite/ControllerDish/releases/latest).

## Discontinued hardware 3.x

Hardware 3.x is discontinued and should only be considered legacy hardware. It has been replaced by the more flexible hardware 2.x platform combined with the dedicated ControllerDish VFD interface module for AC motor installations.

## Hardware images

![ControllerDish hardware](https://github.com/EA3HMJ-Tracking-Software-Suite/ControllerDish/assets/2368602/49b585de-e610-4bf3-919c-1cef5de5cedc)

![ControllerDish installation](https://github.com/EA3HMJ-Tracking-Software-Suite/ControllerDish/assets/2368602/13db4524-f177-49c3-b8c2-e037525d85ba)

![ControllerDish enclosure](https://github.com/EA3HMJ-Tracking-Software-Suite/ControllerDish/assets/2368602/962cf09a-86fe-4725-a146-1549264fb762)

## Documentation

- [Dish Controller v1.2 - English](doc/Dish%20Controller%20v2%20ENG.pdf)
- [Dish Controller v1.4 - English](doc/Dish%20Controller%20v4%20ENG.pdf)
- [Dish Controller v1.5 - English](doc/Dish%20Controller%20v5%20ENG.pdf)
- [Dish Controller v2.2 - Spanish](doc/Dish%20Controller%20V2.2%20ESP.pdf)
- [ControllerDish 2.2 connections - Spanish](doc/Conexiones%20hardware%202.2%20V1.0%20ESP.pdf)
- [Dish Controller v2.3 - Spanish](doc/Dish%20Controller%20V2.3%20ESP.pdf)

## Releases and downloads

- [All releases](https://github.com/EA3HMJ-Tracking-Software-Suite/ControllerDish/releases)
- [Latest release](https://github.com/EA3HMJ-Tracking-Software-Suite/ControllerDish/releases/latest)

## Disclaimer

ControllerDish is an amateur antenna tracking system intended for EME, radio astronomy, amateur DSN, and related applications. Building and operating it requires advanced electronics, electrical, mechanical, and software skills.

All firmware, source code, schematics, and related materials are provided **as is**, without any express or implied warranty. The author cannot provide individual support and shall not be liable for equipment damage, data loss, personal injury, or any other consequences arising from the construction or use of this system.
