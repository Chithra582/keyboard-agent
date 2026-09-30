---
name: "keyboard-hardware-usb-controller"
description: "Discovers, connects, and communicates with Ultimate Hacking Keyboard devices via USB HID."
---

# Keyboard Hardware USB Controller Skill

## Overview
Manages raw hardware discovery and bidirectional packet exchange across USB HID interfaces:
- Identifies connected UHK keyboards and peripheral modules (trackball, touchpad, trackpoint, key cluster).
- Reads hardware descriptors, firmware revisions, and module status packets.
- Dispatches control requests and receives real-time device notifications safely.

## Workflow
1. Enumerate USB devices matching UHK vendor ID (`0x1D50`).
2. Open dedicated HID endpoints for management and diagnostic telemetry.
3. Validate hardware protocol compatibility before sending commands.
4. Cleanly release endpoints upon session termination.
