# Language Selection
[English](README.md) | [Türkçe](README-tr.md)

# BFPTouch Sensor Installation for Ender3 V2

![Demo](Photos/2.gif)

This guide provides detailed instructions to install and configure a low-budget BLTouch clone, the BFPTouch, on your Ender3 V2 printer. The BFPTouch replicates BLTouch functionality and is designed for cost-effective 3D printing enhancements. Follow this guide to achieve successful hardware installation and software configuration.

---

## Overview

The BFPTouch is a budget-friendly alternative to the BLTouch and is designed to work seamlessly with the Ender3 V2. It leverages a 3D-printed mount, a small SG90 servo motor, and an optical endstop to emulate BLTouch capabilities. By printing the mount and completing a few straightforward steps, you can integrate the BFPTouch into your printer setup.

---

## Required Materials

To complete this modification, you will need the following:

- **3D-Printed BFPTouch Mount**
  - Download the mount from Thingiverse: [https://www.thingiverse.com/thing:6918868](https://www.thingiverse.com/thing:6918868)
  - Print the mount using PLA or PETG for best results.
- **1 x SG90 Servo Motor**
- **1 x Optical Endstop**
- **Soldering Tools**: Soldering iron, solder, and flux (if needed).
- **Basic Tools**: Screwdrivers, pliers, and cable ties.

---

## Hardware Installation

1. **Print the BFPTouch Mount**:
   - Download the 3D model from the provided Thingiverse link.
   - Print the model using your preferred 3D printer. Ensure the print quality is high to allow proper component fitting.

2. **Assemble the Components**:
   - Insert the SG90 servo motor into its designated slot in the printed mount.
   - Secure the optical endstop in the provided slot.
   - Route the wires neatly to prevent interference with printer movement.

3. **Mount the BFPTouch to the Printer**:
  - Attach the printed mount with the installed components to your Ender3 V2 using a tight-fit design instead of screws.
   - Ensure the mount is securely in place with the tight-fitting design.

     <img src="Photos/4.jpg" width="200" />  <img src="Photos/2.jpg" width="200" /> <img src="Photos/3.gif" width="266" />
   
4. **Connect the Wiring**:
   - Follow the wiring connections below to complete the setup:

     ```
     +------------------+-----------------------------+
     | Mainboard Pin    | BFPTouch Pin                |
     +------------------+-----------------------------+
     | V                | SG90 VCC, Optic Endstop VCC |
     | G                | SG90 GND, Optic Endstop GND |
     | IN               | SG90 PWM Signal             |
     | OUT              | Optic Endstop Output        |
     +------------------+-----------------------------+
     ```
   - Ensure all connections are secure and insulated to avoid short circuits.

---

## Why Special Configuration is Required for BFPTouch?

Normally, the working principle of the BFPTouch differs from that of the BLTouch. The BLTouch interprets certain servo signal angles from the mainboard not as direct angle commands but as instructions for specific operations, thanks to a microcontroller on the sensor. Below is a visual representation showing which angle values correspond to which commands for the BLTouch:

<img src="Photos/6.png" width="800" />

In contrast, the BFPTouch lacks any onboard controller, and the servo signal received from the mainboard directly controls the angle of the SG90 servo motor. Due to the mechanical design of the BFPTouch, the angle values corresponding to BLTouch commands can result in unintended mechanical collisions. Therefore, we need to adjust certain configurations in the firmware to make it compatible with the BFPTouch.

---

## Software Configuration

There are two methods to configure your Ender3 V2 firmware for BFPTouch functionality:

### Option 1: Use Pre-Compiled Firmware

Download and flash the pre-configured firmware from the provided repository link. This is the simplest method for most users.

Repository Link: [https://github.com/sezgynus/Ender3V2S1](https://github.com/sezgynus/Ender3V2S1)

### Option 2: Manually Configure Marlin Firmware

If you prefer to configure and build the firmware yourself, follow the detailed instructions provided in the next section. Ensure you have the Marlin source code and a compatible build environment ready.

---

Stay tuned for the next steps to complete your BFPTouch installation and software setup!

