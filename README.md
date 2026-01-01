# ZMK Firmware for Custom Dactyl Manuform Keyboard

A custom firmware configuration for my hand-built Dactyl Manuform split wireless Bluetooth keyboard, built with [ZMK](https://zmk.dev/) firmware. This keyboard is my daily driver for software development and coding.

## Overview

This repository contains the complete ZMK firmware configuration for a custom 5x6 thumb cluster Dactyl Manuform keyboard. The keyboard features:

- **Split ergonomic design** - Two independent halves for optimal hand positioning
- **Wireless Bluetooth connectivity** - Powered by Seeed XIAO BLE microcontrollers
- **5x6 key matrix** - 5 rows × 6 columns per half with thumb clusters
- **Multi-layer keymap** - Custom layers for navigation, media control, and Bluetooth management
- **Advanced behaviors** - Tap-dance, combos, hold-tap, and sensor-based scrolling
- **Mouse integration** - Built-in mouse key support for cursor control

## Hardware

- **Controllers**: Seeed XIAO BLE (nRF52840-based)
- **Layout**: 5 rows × 6 columns per half (60 keys total)
- **Connectivity**: Bluetooth Low Energy (BLE)
- **Battery**: Integrated battery monitoring via nRF VDDH

## Key Features

### Custom Behaviors

The firmware implements several custom behaviors to enhance productivity:

- **Tap-Dance**: Double-tap backspace for delete
- **Hold-Tap Combinations**: 
  - Layer-tap-or-mouse: Tap for mouse click, hold for layer access
  - Momentary-and-toggle: Hold for layer, tap to toggle
  - Momentary-and-keypress: Hold for layer, tap for key
- **Scroll Encoder**: Sensor-based scrolling in four directions
- **Key Combos**: Volume control via simultaneous key presses

### Layer System

1. **Default Layer**: Standard QWERTY layout with ergonomic modifications
2. **Layer 1**: Function keys, mouse controls, navigation, and media
3. **Layer 2**: Bluetooth device management and additional navigation
4. **Scroll Layer**: Media playback controls and workspace navigation
5. **Snipe Layer**: Minimal layer for precise navigation

### Ergonomic Optimizations

- **Mirrored thumb clusters**: Optimized thumb key placement
- **Home row mods**: Shift, Ctrl, Alt, and GUI on home row
- **Layer-tap keys**: Access layers without moving hands
- **One-handed operation**: Full functionality accessible from either half

## Project Structure

```
config/
├── boards/shields/xiao_flex_v2/    # Shield definitions and hardware config
│   ├── xiao_flex_v2.dtsi           # Device tree source (matrix, GPIO)
│   ├── xiao_flex_v2_left.conf      # Left half configuration
│   └── xiao_flex_v2_right.conf     # Right half configuration
├── xiao_flex_v2.keymap             # Main keymap with all layers and behaviors
├── xiao_flex_v2.conf               # ZMK configuration (BLE, RGB, etc.)
└── west.yml                        # Zephyr/zmk dependency management
```

## Building

This project uses ZMK's build system with GitHub Actions for automated firmware builds.

### Prerequisites

- [Zephyr SDK](https://docs.zephyrproject.org/latest/getting_started/index.html)
- [West](https://docs.zephyrproject.org/latest/develop/west/index.html) (Zephyr's meta-tool)
- ZMK firmware repository

### Build Commands

```bash
# Initialize west workspace
west init -l config
west update

# Build left half
west build -s zmk/app -b seeeduino_xiao_ble -- -DSHIELD=xiao_flex_v2_left -DZMK_CONFIG="$(pwd)/config"

# Build right half
west build -s zmk/app -b seeeduino_xiao_ble -- -DSHIELD=xiao_flex_v2_right -DZMK_CONFIG="$(pwd)/config"
```

Firmware files will be generated in `build/zephyr/zmk.uf2` for each half.

## Configuration Highlights

### Bluetooth Settings

- Experimental connection features enabled
- Optimized BLE parameters for low latency
- Support for multiple device pairing (up to 3 devices)
- Battery monitoring via nRF VDDH

### Matrix Configuration

- **5 rows × 12 columns** (6 per half)
- Column-to-row diode direction
- GPIO-based matrix scanning
- Optimized pin assignments for XIAO BLE

### Keymap Features

- **Mod-tap keys**: Layer access without dedicated keys
- **Combo support**: Volume up/down via key combinations
- **Mouse keys**: Full mouse control (left, right, middle click)
- **Media controls**: Play/pause, next/previous track, volume
- **Navigation**: Arrow keys, home/end, workspace switching

## Technical Details

### Embedded Systems Development

- **Firmware**: ZMK (Zephyr-based keyboard firmware)
- **Language**: Device Tree Source (DTS) for hardware configuration
- **Build System**: Zephyr RTOS build system with CMake
- **Bluetooth Stack**: Nordic nRF Connect SDK BLE stack

### Custom Behaviors Implementation

The firmware implements complex key behaviors using ZMK's behavior system:

- **Tap-dance**: Multi-tap detection with configurable timing
- **Hold-tap**: Dual-function keys with customizable timing and flavors
- **Sensor bindings**: Rotary encoder support for scrolling
- **Combo engine**: Simultaneous key press detection

## Usage

This keyboard is my primary input device for:
- Software development and coding
- System administration
- General computer use

The ergonomic design and custom keymap significantly reduce hand strain during long coding sessions.

## Development Notes

- **Branch**: `5x6-tb` (5x6 thumb cluster layout)
- **ZMK Version**: Custom fork with pointer/scroll features
- **Driver**: PMW3610 sensor driver for scroll functionality

## License

This configuration is released under the MIT License, following ZMK's licensing.

---

**Built with**: ZMK Firmware, Zephyr RTOS, nRF Connect SDK  
**Hardware**: Custom Dactyl Manuform, Seeed XIAO BLE

