# Ender 3 V2 Upgrade Guide

[English](README.md) | [Türkçe](README-tr.md)

A practical collection of documented hardware and firmware modifications for the **Creality Ender 3 V2**. The repository focuses on upgrades that were implemented on real hardware and preserves the wiring, configuration, schematics, photographs, and demonstrations required to reproduce them.

## Project Overview

The guide currently documents three upgrade areas:

| Upgrade | Purpose | Documentation |
|---|---|---|
| [BFPTouch Sensor](./BFPTouch_Sensor/README.md) | Add low-cost automatic bed probing using an SG90 servo and optical endstop | Hardware installation, wiring, firmware approach, photos and demonstrations |
| [Case Light](./Case_Light/README.md) | Add firmware-controlled 24 V case lighting to the Ender 3 V2 mainboard | Mainboard modification, schematic, Marlin configuration and assembly photos |
| [Filament Sensor](./Filament_Sensor/README.md) | Add filament-presence detection | Installation photos and demonstration assets |

The repository is organized as a set of independent modifications. Each documented upgrade can be reviewed separately without requiring the others.

## At a Glance

| Area | Implementation |
|---|---|
| Target printer | Creality Ender 3 V2 |
| Firmware | Marlin |
| Automatic bed probing | BFPTouch / BLTouch-style functionality |
| Probe hardware | SG90 servo + optical endstop |
| Case-light control | MCU PA3 → HC245 → MOSFET |
| Case-light supply | 24 V |
| Case-light command | Marlin `M355` |
| Brightness range | 0–255 |
| Documentation | English and Turkish |
| Supporting material | Schematics, wiring information, photos and GIF demonstrations |

## Upgrade Guides

### 1. BFPTouch Sensor

[Open the BFPTouch installation guide →](./BFPTouch_Sensor/README.md)

The BFPTouch modification provides BLTouch-style probing using a 3D-printed mount, an **SG90 servo motor**, and an **optical endstop**. Because the BFPTouch does not contain the controller used by a BLTouch, the servo signal directly controls the mechanical angle and requires compatible firmware configuration.

The existing guide includes:

- component and mounting requirements;
- Ender 3 V2 mainboard wiring;
- explanation of the BFPTouch/BLTouch control difference;
- pre-configured firmware and manual Marlin configuration paths;
- installation photographs and animated demonstrations.

![BFPTouch demonstration](BFPTouch_Sensor/Photos/2.gif)

### 2. Case Light Control

[Open the case-light modification guide →](./Case_Light/README.md)

The Ender 3 V2 mainboard does not provide a dedicated case-light output, although Marlin supports case-light control. This modification repurposes the **PA3** MCU pin and uses an unused HC245 channel together with an external N-channel MOSFET to switch a **24 V LED load**.

The documented signal path is:

```text
MCU PA3
   │
   ▼
RP6 resistor network
   │
   ▼
Unused HC245 channel
   │
   ▼
10 Ω series resistor
   │
   ▼
N-channel MOSFET
   │
   ▼
24 V case light
```

The guide includes the mainboard modification schematic, component selection, soldering references, assembly photographs, and the required Marlin settings.

![Case-light modification schematic](Case_Light/HW_Modifications/Modification_Schemetic.png)

#### Marlin Control

Case-light control is exposed through Marlin's `M355` command:

```text
M355 [P<byte>] [S<bool>]
```

- `P<byte>`: brightness from **0 to 255**
- `S<bool>`: light on/off state

The firmware configuration also documents menu control, optional fast PWM at **31.4 kHz**, startup state, and default brightness.

### 3. Filament Sensor

[Open the filament-sensor directory →](./Filament_Sensor/README.md)

The filament-sensor section documents the evidence currently available in the repository: installation photographs and an animated demonstration. The sub-guide deliberately limits itself to those verified materials; wiring and firmware details are not inferred where the repository does not provide them.

## Documentation Approach

The material in this repository is based on implemented modifications rather than a generic list of possible Ender 3 V2 upgrades. The documentation separates the work into four layers where material is available:

```text
Hardware modification
        ↓
Electrical / wiring reference
        ↓
Firmware configuration
        ↓
Physical installation and verification
```

This makes it possible to inspect both the implementation and the reasoning behind the modification instead of relying only on a finished firmware binary.

## Firmware

The BFPTouch and case-light guides provide two firmware paths:

1. use the referenced pre-configured firmware;
2. apply the documented changes manually to Marlin and build the firmware.

The pre-configured firmware referenced by the guides is maintained separately in the `sezgynus/Ender3V2S1` repository. Manual configuration is documented inside the relevant upgrade guide so that the hardware modifications are not tied exclusively to a pre-built binary.

## Repository Structure

```text
Ender3-V2-Upgrade-Guide/
├── BFPTouch_Sensor/
│   ├── Photos/
│   ├── README.md
│   └── README-tr.md
├── Case_Light/
│   ├── Diagrams/
│   ├── HW_Modifications/
│   ├── Photos/
│   ├── README.md
│   └── README-tr.md
├── Filament_Sensor/
│   ├── Photos/
│   ├── README.md
│   └── README-tr.md
├── LICENSE
├── README.md
└── README-tr.md
```

## Project Status

| Area | Status |
|---|---|
| BFPTouch hardware installation | Documented |
| BFPTouch wiring | Documented |
| BFPTouch firmware approach | Documented |
| Case-light hardware modification | Documented |
| Case-light Marlin configuration | Documented |
| Case-light assembly references | Documented |
| Filament-sensor media | Available |
| Filament-sensor media guide | Documented from available repository material |

No undocumented technical details have been inferred in this overview; the status reflects the material currently stored in the repository.

## Safety

The case-light modification requires soldering directly to the printer mainboard and switches a 24 V load. Disconnect the printer from power before modifying the board, verify the schematic and wiring before power-up, and ensure that the selected MOSFET and LED hardware are suitable for the electrical conditions described in the guide.

## License

This project is licensed under the [MIT License](LICENSE).
