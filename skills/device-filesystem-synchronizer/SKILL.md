---
name: "device-filesystem-synchronizer"
description: "Synchronizes user keymaps, layers, and configuration trees with on-device EEPROM flash memory."
---

# Device Filesystem Synchronizer Skill

## Overview
Maintains the on-device filesystem (`uhk-fs`) stored in keyboard EEPROM:
- Organizes configuration profiles, keymaps, and module parameters.
- Implements differential write algorithms to minimize flash memory wear.
- Verifies sector checksums post-write to ensure zero data corruption.

## Key Features
- Transactional state journaling.
- Atomic commit boundaries.
- Offline layout serialization for backup and restore.
