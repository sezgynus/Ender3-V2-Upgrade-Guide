# Language Selection
[English](README.md) | [Türkçe](README-tr.md)

# Ender 3 V2 Upgrade Guide

Welcome to the **Ender 3 V2 Upgrade Guide**! This repository provides detailed instructions and resources to enhance your Ender 3 V2 3D printer with some amazing upgrades. Each upgrade includes hardware setup, software configuration, and helpful tips to ensure a smooth experience.

---

## 🚀 Available Upgrades

### [1. **BFPTouch Sensor Installation**](./BFPTouch_Sensor)
Enhance your 3D printer with automatic bed leveling for better print quality and ease of use.

- **Features**: Improved first-layer consistency, hassle-free bed leveling.
- **Resources**: 
  - Installation guide
  - Firmware configuration
  - Wiring diagrams
  - Photos for reference

### [2. **Case Light Activation and LED Output Modification**](./Case_Light)
Illuminate your workspace and modify the mainboard for LED control.

- **Features**: Integrated lighting for better print visibility.
  - **G-code control**: Control the case light via G-code with `M355`:
    - **Usage**: `M355 [P<byte>] [S<bool>]`
    - **Parameters**:
      - `[P<byte>]`: Set the brightness factor from 0 to 255.
      - `[S<bool>]`: Turn the case light on or off.
    - For detailed documentation, visit the [Marlin M355 G-code page](https://marlinfw.org/docs/gcode/M355.html).
  - **Flexible control options**:
    - Add `M355` macros to the G-code generated by your slicer to automate light control during prints.
    - Use OctoPrint custom controls to trigger the macro and adjust the lighting via the user interface for greater flexibility.
- **Resources**:
  - Wiring modifications
  - Circuit diagrams
  - Photos of the setup

### [3. **Filament Sensor Installation**](./Filament_Sensor)
Avoid failed prints by installing a filament sensor to detect when filament runs out or breaks.

- **Features**: Real-time filament monitoring.
- **Resources**:
  - Installation instructions
  - Firmware updates
  - Circuit connections

---

## 🛠️ What You'll Find Here
This repository contains:

1. **Detailed Instructions**: Step-by-step setup guides for each upgrade.
2. **Firmware Resources**: Precompiled firmware and source code for customization.
3. **Circuit Diagrams**: Clear diagrams for wiring and connections.
4. **Photos**: High-resolution images for reference during installation.
5. **Troubleshooting Tips**: Common issues and their solutions.

---

## 📂 Repository Structure
```
📁 Ender3V2_Upgrade_Guide
├── BFPTouch_Sensor
│   ├── README.md
│   ├── README-tr.md
│   ├── Diagrams
│   └── Photos
├── Case_Light
│   ├── README.md
│   ├── README-tr.md
│   ├── HW_Modifications
│   ├── Diagrams
│   └── Photos
├── Filament_Sensor
│   ├── README.md
│   ├── README-tr.md
│   ├── Diagrams
│   └── Photos
├── README.md
└── README-tr.md
```

---

## 📜 License
This project is licensed under the [MIT License](LICENSE).

---

## 🙌 Contributions
Contributions are welcome! If you have ideas for new upgrades, improvements, or fixes, feel free to open an issue or submit a pull request.

---

Happy printing! 🎉
