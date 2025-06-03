# Creality-Laser-Module-1.6W_Ender3V2_Klipper

A step-by-step guide to connecting and configuring the Creality 1.6W Laser Module on an Ender 3 V2 running Klipper firmware. Includes wiring diagrams, configuration files, safety tips, and test results.

---

## ⚠️ Disclaimer

This project involves hardware modifications and the use of a laser module. It is intended for educational and non-commercial use only. Use at your own risk.

The author is not responsible for any damage, injury, or legal issues resulting from the use of this guide or any files provided in this repository. Always follow laser safety guidelines and check local laws before use.

---

## 🛠️ Software Requirements

- [LightBurn](https://lightburnsoftware.com/) – for creating laser G-code.
- Any basic text editor (e.g. VS Code, Notepad++, Sublime Text).
- Klipper firmware – already installed on your Ender 3 V2.
- ✅ A ready-to-use laser configuration file for Klipper is included in this repository.

> Note: This setup uses a **BL-Touch** instead of the stock Z endstop — already accounted for in the config.

---

## 🔌 Laser Module Wiring

The Ender 3 V2 printhead includes two fans:

1. **Part Cooling Fan** – controlled by PWM during printing.
2. **Hotend Heatsink Fan** – always on, provides constant 24V.

The Creality 1.6W laser requires three connections:
- `VCC` – 24V power
- `GND` – ground
- `PWM` – control signal

### ⚠️ Important Notes:

- Use `VCC` and `GND` from the **always-on fan** (Fan 2). Disconnect that fan to access constant 24V power.
- The `PWM` signal should be connected to the **GND (-)** wire of the **part cooling fan** (Fan 1). That’s where the PWM signal is actually delivered.

> ❗ **DO NOT** connect the PWM wire from the laser to the **+ (positive)** wire of the fan — this can burn the laser's internal diode.  
If that happens, simply replace the damaged diode with a new one.

---

## ⚙️ Klipper Configuration

1. Replace your current `printer.cfg` with the provided **`LASER printer.cfg`** from this repository.
2. Rename the file to `printer.cfg` before uploading it to Klipper.
3. It is highly recommended to **backup your 3D printing config** beforehand to allow easy switching between modes.

---

## 🧾 Preparing G-code in LightBurn

1. Create your laser engraving design in **LightBurn**.
2. Export the `.gcode` file.
3. Open the file in a text editor or use the provided Python tool.
4. Replace all `F0` commands (which are not allowed in Klipper) with `F800`, `F600`, or another appropriate feedrate.

> In VS Code, press `Ctrl + H` to find and replace all instances of `F0`.

---

## 🔥 Starting the Engraving

Once everything is set up:

1. Upload your corrected `.gcode` file to Klipper via Mainsail/Fluidd.
2. Start the print as you would for a normal 3D print.

> The process is identical to launching a 3D print, so it should feel familiar.

---

## 📂 Repository Contents

- `LASER printer.cfg` – ready-to-use Klipper config for laser mode.
- `lightburn-config/` – LightBurn settings for optimal performance.
- `photos/` – wiring photos (optional).
- `klipper_config/` – additional config fragments or macros.
- `tools/` – optional Python script for G-code cleanup.

---
