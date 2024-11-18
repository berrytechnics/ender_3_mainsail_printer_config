# Klipper Configuration for BIGTREETECH SKR mini E3 v2.0

This configuration is for a 3D printer using the BIGTREETECH SKR mini E3 v2.0 board with BLTouch auto-leveling.

## Hardware Specifications

- Control Board: BIGTREETECH SKR mini E3 v2.0
- Build Volume: 235x235x250mm
- Auto-leveling: BLTouch
- Stepper Drivers: TMC2209 (UART mode)
- Display: ST7920 compatible

## Features

- Auto bed leveling with BLTouch
- Mesh bed leveling (5x5 grid)
- Screw tilt adjustment assistance
- Stealth mode enabled (StealthChop)
- Filament load/unload macros
- Print start/end sequences
- Mainsail web interface support

## Installation

1. Copy this configuration to your Klipper config directory
2. Ensure `mainsail.cfg` is present in the same directory
3. Verify your MCU serial path matches the one in the config:
   ```
   serial: /dev/serial/by-id/usb-Klipper_stm32f103xe_31FFD5054250373922500257-if00
   ```

## Usage

### Starting a Print

The START_PRINT macro handles:
- Bed and extruder heating
- Auto bed leveling
- Nozzle priming

Use in your slicer start G-code:
```
START_PRINT BED_TEMP=[first_layer_bed_temperature] EXTRUDER_TEMP=[first_layer_temperature]
```

### Loading Filament

```
LOAD_FILAMENT TEMP=200
```
Adjusts temperature and loads filament.

### Unloading Filament

```
UNLOAD_FILAMENT TEMP=200
```
Adjusts temperature and retracts filament.

### Bed Leveling

1. Home printer: `G28`
2. Run screw adjustment: `SCREWS_TILT_ADJUST`
3. Follow on-screen instructions to level bed corners
4. Run bed mesh calibration: `BED_MESH_CALIBRATE`

## Important Settings

- Max Speed: 300mm/s
- Max Acceleration: 3000mm/s²
- Max Z Speed: 5mm/s
- Probe Offsets:
  - X: -45mm
  - Y: -4mm
  - Z: 2.745mm

## Safety Features

- Minimum temp: 0°C
- Maximum temps:
  - Extruder: 250°C
  - Bed: 130°C
- Endstop protection
- Motor current limits configured for reliability

## Troubleshooting

If you encounter "Unknown command: EXCLUDE_OBJECT_DEFINE", add this to your config:
```
[exclude_object]
```

For BLTouch probe issues, verify:
- Probe offset values
- Wiring connections
- Pin assignments (sensor_pin: ^PC14, control_pin: PA1)
