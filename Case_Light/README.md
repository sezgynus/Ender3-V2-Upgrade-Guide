# Case Light Control — Ender 3 V2

[English](README.md) | [Türkçe](README-tr.md) | [← Main Guide](../README.md)

This guide documents a hardware modification that adds **firmware-controlled 24 V case lighting** to an Ender 3 V2 mainboard. The implementation repurposes the MCU's **PA3** pin, routes it through an unused HC245 channel, and drives the LED load with an external N-channel MOSFET.

> **Hardware modification:** this procedure requires soldering directly to the printer mainboard. Disconnect all power before working on the board and verify every connection before power-up.

## At a Glance

| Area | Implementation |
|---|---|
| Target printer | Creality Ender 3 V2 |
| Firmware | Marlin |
| MCU control pin | PA3 |
| Buffer | Unused HC245 channel |
| MOSFET gate resistor | 10 Ω |
| Gate pulldown | 100 kΩ |
| LED supply | 24 V |
| Control command | `M355` |
| Brightness range | 0–255 |
| Optional fast PWM | 31.4 kHz |

## Design

The Ender 3 V2 mainboard does not expose a dedicated case-light output, while Marlin already provides case-light control. The modification therefore adds the missing power-output stage around an unused processor signal.

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
N-channel MOSFET gate
   │
   ├── 100 kΩ pulldown → GND
   │
   ▼
24 V LED load
```

![Modification schematic](HW_Modifications/Modification_Schemetic.png)

The repository also contains the Creality 4.2.2 schematic used as a board reference in `Diagrams/Creality.4.2.2.-.Schematic.pdf`.

## Required Components

- **1 × 100 kΩ resistor**
- **1 × 10 Ω resistor**
- **1 × N-channel MOSFET**, rated for at least 30 V drain-source voltage
  - HY1403: device type already used on the Ender 3 V2 for heater switching
  - FR024N: documented alternative
- Soldering iron, solder and flux
- Optional breakout board for the MOSFET
- **24 V LED lighting**

The documented circuit switches the 24 V rail, so the connected lighting must be suitable for 24 V operation.

## Hardware Modification

### 1. PA3 Connection

Route the MCU's **PA3** signal to the empty channel of the RP6 resistor network.

### 2. HC245 Connection

Route the signal from RP6 through an unused HC245 transceiver channel. The documented implementation prefers the A3/B3 channel pair when available.

### 3. Gate Series Resistor

Connect the HC245 output to the MOSFET gate through a **10 Ω** series resistor.

### 4. Gate Pulldown

Connect a **100 kΩ** pulldown resistor between the MOSFET gate and GND.

### 5. MOSFET Power Path

- MOSFET source → GND
- MOSFET drain → LED negative terminal
- LED positive terminal → 24 V

### 6. Verify Before Power-Up

Compare all added connections with the modification schematic before applying power.

## Assembly Reference

![Overall modification setup](Photos/1.jpg)

![Close-up of soldering details](Photos/2.jpg)

The photographs show the connections up to the MOSFET gate. In the documented implementation, the MOSFET itself is connected using flying leads and is therefore not visible in these photographs.

## Firmware Configuration

Two firmware paths are available.

### Option 1 — Pre-configured Firmware

A firmware build containing the required configuration is referenced in the separate [Ender3V2S1 repository](https://github.com/sezgynus/Ender3V2S1).

### Option 2 — Manual Marlin Configuration

The following settings are documented for manual configuration.

#### 1. Enable Case Light

In `Configuration_adv.h`:

```cpp
//#define CASE_LIGHT_ENABLE
#define CASE_LIGHT_ENABLE
```

#### 2. Assign PA3

```cpp
//#define CASE_LIGHT_PIN 4
#define CASE_LIGHT_PIN PA3
```

#### 3. Enable Menu Control

```cpp
//#define CASE_LIGHT_MENU
#define CASE_LIGHT_MENU
```

With menu control enabled:

<p>
  <img src="Photos/6.jpg" width="45%" />
  <img src="Photos/7.jpg" width="45%" />
</p>

#### 4. Optional Fast PWM

To reduce visible flicker at low brightness:

```cpp
//#define FAST_PWM_FAN
#define FAST_PWM_FAN
```

#### 5. Set Fast PWM Frequency

```cpp
//#define FAST_PWM_FAN_FREQUENCY 31400
#define FAST_PWM_FAN_FREQUENCY 31400
```

This configures the documented **31.4 kHz** PWM frequency.

#### 6. Set Startup State

```cpp
#define CASE_LIGHT_DEFAULT_ON true
#define CASE_LIGHT_DEFAULT_ON false
```

Use the desired value: `true` starts with the light enabled; `false` starts with it disabled.

#### 7. Set Default Brightness

```cpp
#define CASE_LIGHT_DEFAULT_BRIGHTNESS 105
#define CASE_LIGHT_DEFAULT_BRIGHTNESS 255
```

The valid brightness range is **0–255**.

## G-code Control

Marlin exposes case-light control through `M355`:

```text
M355 [P<byte>] [S<bool>]
```

- `P<byte>`: brightness, 0–255
- `S<bool>`: on/off state

This allows the light to be controlled manually, from printer interfaces that expose the command, or through G-code generated around a print workflow.

## Verification Checklist

Before normal use:

- confirm the PA3-to-HC245 routing against the schematic;
- verify the 10 Ω gate resistor and 100 kΩ pulldown;
- verify MOSFET source, drain and gate connections;
- confirm the LED load is rated for 24 V;
- inspect for solder bridges and unintended shorts;
- test on/off control before relying on brightness control;
- verify `M355` and menu behavior after flashing the configured firmware.

## Safety

Incorrect wiring can damage the mainboard or connected lighting. Perform all soldering with the printer disconnected from power. The documented MOSFET voltage requirement and 24 V load requirement should be treated as minimum design constraints rather than optional substitutions.

[← Return to the main upgrade guide](../README.md)
