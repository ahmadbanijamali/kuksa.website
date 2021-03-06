+++
title = "Automotive Ethernet Gateway by taskit"
date = "2019-10-28"
tags = ["taskit", "gateway"]
categories = ["use-cases"]
banner = "img/clients/Taskit-320x180.png"
author = "Nikolai Ostapowicz"
+++

**taskit GmbH** has developed a Car2X Gateway, which enables standardized, secure access to the cloud for in-car software. It comes pre-installed with Automotive Grade Linux (AGL) and Eclipse Kuksa and supports multiple interfaces such as CAN bus and Automotive Ethernet.

<p style="text-align:center;">
 <a href="/kuksa/blog/images/2019-10-28-taskit-01.jpg">
   <img src="/kuksa/blog/images/2019-10-28-taskit-01.jpg" width="60%" alt="Automotive Ethernet Gateway"/>
 </a><br/>
 <strong>Figure 1: Automotive Ethernet Gateway</strong>
</p>

The Gateway was created as a part of the APPSTACLE project. This project is creating an open de facto standard and an open-source implementation of a complete technology stack for connected car scenarios as well as an associated ecosystem of libraries, tools, business models, services and support - hosted by the Eclipse Foundation as the Eclipse Kuksa project. The development of connected cars is promoted by the provision of relevant components, e.g. for the decentralized management of automotive data as well as various innovative features such as OTA (Over-the-Air) ECU upgrades.
The automotive (in-car) system is a system of interface definitions (APIs), software libraries, communication stacks, and development tools, that allow automotive ECUs to securely connect to an IoT platform via a communication gateway. The API is designed to allow installation and maintenance of applications over the air (OTA) via standard interfaces, taking into account requirements of safety-critical components such as authentication and data security. In this context, taskit GmbH has developed a Car2X Gateway, which enables standardized access to the cloud for in-car software. This gateway supports comprehensive data exchange with other internal systems or ECUs and allows for cross-controller connectivity with the “outside world”. Flexibility is provided by enabling multiple interfaces such as CAN bus and Automotive Ethernet. The gateway was developed with the goal to foster wide adoption of open standards in both legacy and new systems. Therefore, by default, it comes with preinstalled Automotive Grade Linux (AGL) and implementation of Eclipse Kuksa. 

# Use Cases
The board is highly flexible. For example, it can be applied as a smart gateway for BLE-receiving units like the Beacon Line. With the Beacon Line, it is possible to cover hundreds of square meters with BlueTooth Low Energy (BLE) with only a small kit of Beacon Line Nodes and one Gateway. Another application area is public transport, where customers use e-tickets to hop on and hop off. Every customer pays only for the number of stations traveled instead of buying a time-based ticket. The gateway provides all the features to efficiently implement this system: Dual-SIM LTE modem to stay connected, GPS to track locations and of course a serial port to activate the beacon line features. Tour logs and related ticket prices can then be calculated on backend servers.

# Technical Data

<p style="text-align:center;">
 <a href="/kuksa/blog/images/2019-10-28-taskit-02.jpg">
   <img src="/kuksa/blog/images/2019-10-28-taskit-02.jpg" width="60%" alt="Hardware Overview "/>
 </a><br/>
 <strong>Figure 2 Hardware Overview </strong>
</p>

 
# CPU
* taskit “DropA5D22” CPU module
* The module contains a "SAMA5D36" processor from Microchip, with an ARM Cortex-A5 Core, 498 MHz Clock rate

# Memory
* 256MB LPDDR RAM
* 2MB serial NOR-Flash (64MB optional), part of the CPU module
* 512MB serial (quad-SPI) NAND-Flash (optional), as part of the baseboard

# Interfaces
* MicroSD Card Slot
* Ethernet 10/100Base-T (RJ-45)
* 3x Automotive Ethernet, Molex MD50 Connectors
* LTE-Modem "Gemalto ALS3-E", dual SIM, GPS
* 3xUSB-Host (2x USB-A connector, 1x 4-pin header)
* USB-Device (USB-B connector)
* Dual CAN - one 9-pin male D-type connector
* 2x I/O-Jack - 6-pin RJ12 connector with UART/I²C/SPI/GPIO/VCC signals, 3.3V levels
* 1x RS422/RS485 - 8-pin RJ45 connector
* TFT up to 800x480 resolution
* Touchscreen capacitive or resistive
* Expansion Slot, 10x2 pin header (2mm pitch), including JTAG-interface and tamper-protection pins

## Power Supply
* 8 ... 24V DC recommended, 42V Maximum Rating
* Protection against Reverse Polarity
* 2-pole "PicoMax" terminal block (X5)
* Overvoltage Protection (e. g. in case of "Load Dump"): Suppressor Diodes for up to 2200 W peak pulse power at a 10ms x 150ms test waveform
* 5A resettable fuse (F5)
* Optional Power Supply via CAN Interface or AE Interface: 2A fast-acting fuses on each Interface (F1, F2, F3, F4)

### Power Consumption
* 4W Linux idle, 8W peak, including TFT, Ethernet and AE active, but without LTE Modem
* LTE Modem:
** < 5W GSM, HSDPA, LTE
** < 15W  peak power during GSM transmit burst at "voice call GSM900" - this is not supposed to apply here, but not 100% tested

## Special features
* Real-Time Clock (RTC) with a backup battery
* Cryptographic features
* Tamper protection

## Operating System
* Linux 4.9 kernel (currently)
* Eclipse Kuksa root file system
* Alternatively: Debian 8 (“Jessie”)

The operating system usually resides on the SD card, but may also be installed in flash memory.

Booting is carried out as a 4-stage procedure:
* 1st level: ROM loader
* 2nd level: Serial flash loader (within NOR-flash)
* 3rd level: Linux or other, from SD card or NAND- or NOR-flash.

The first level bootload (ROM loader) is part of the CPU chip and cannot be altered. The second level loader is a small program (e.g. 20k) which provides initialization of the RAM controller as well as some of the interfaces. It looks for a valid Linux kernel image file on the first partition of the SD card. This program is available as a source code and may be altered by users if necessary

## Ethernet and Automotive Ethernet
The APPSTACLE Gateway contains one standard 100Base-T Ethernet port ("ETH 100") and three Automotive Ethernet ports (AE1, AE2, AE3). These are connected to the Ethernet MAC of the CPU by IC1, an "Automotive Ethernet Switch" from NXP, namely the SJA1105EL.
The automotive Ethernet ports AE1 and AE2 are configured as "Master" via SMD jumper, AE3 as "Slave". The "Master" initializes the link in case of a cable connection, so a slave-to-slave connection will not work.
The SJA1105EL switch is by default in a promiscuous mode. Each packet that arrives on one of the five ports is forwarded to all four of the other ports. This behavior can be modified in various ways using the "sja1105-tool".

## Resources
* <a href="data/AGL for taskit GmbH Appstacle Gateway.zip">The Software-Package</a>
* <a href="data/Shortform_english_.pdf">How do you get start with the Appstacle Project Board</a>
* <a href="data/2019_01_17_appstacle_project_board_003.pdf">Appstacle Project Board presentation by taskit</a>
* <a href="data/2018_02_28_APPSTACLE_oulu_taskit_hardware.pdf">Appstacle Project Board hardware presentation by taskit</a>
* <a href="data/DropA5D22_technicalreference.pdf">DropA5D22: Technical Reference</a>

### For any questions, please contact:
* **taskit GmbH**
* Mail: nostapowicz(AT)taskit.de
* Web: www.taskit.de
 
## About taskit GmbH
**taskit GmbH** distinguishes itself above all by short service paths and flexible adaptation to new requirements. The flexibility to realize solutions with low overhead has a liberating effect on large companies. For new technologies, a simple pre-series development project or prototype construction for evaluation of concepts can be cost-effective and easy to implement with the taskit team.