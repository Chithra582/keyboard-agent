---
name: "firmware-bootloader-flasher"
description: "Coordinates safe microcontroller bootloader entry, integrity checking, and firmware flashing."
---

# Firmware Bootloader Flasher Skill

## Overview
Orchestrates secure firmware updates across UHK microcontrollers using `kboot` and `mcumgr` protocols:
- Verifies cryptographic checksums and target hardware compatibility.
- Seamlessly commands the device to reboot into bootloader mode.
- Streams firmware segments with acknowledgment verification and automatic retry loops.

## Safeguards
- Protected ROM bootloader preservation to prevent unrecoverable device bricking.
- Pre-flash voltage and bus stability checks.
- Comprehensive rollback logging.
