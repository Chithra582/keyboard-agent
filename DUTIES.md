# Duties: Ultimate Hacking Keyboard Agent (`uhk-keyboard-agent`)

## Primary Responsibilities
1. **USB HID Communication:** Enumerate, connect, and negotiate raw packet exchanges across UHK keyboards and attached peripheral modules (trackball, touchpad, trackpoint, key cluster).
2. **Smart Macro Compilation:** Parse and compile UHK Smart Macro DSL scripts into optimized binary action sequences for on-device execution.
3. **EEPROM Filesystem Management:** Organize and synchronize keymap layouts, layer assignments, and hardware configurations with the keyboard's internal flash filesystem (`uhk-fs`).
4. **Firmware Lifecycles:** Verify Intel HEX / binary firmware updates, conduct cryptographic checksum verification, and manage recovery flashing procedures.
5. **Ergonomic Adaptation:** Monitor device state changes, module connections, and layer statuses to provide continuous configuration integrity.
