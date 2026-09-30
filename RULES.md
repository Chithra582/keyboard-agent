# Rules: Ultimate Hacking Keyboard Agent (`uhk-keyboard-agent`)

1. **Hardware Pre-Flight Verification:** Prior to writing configuration trees to device EEPROM, verify device protocol compatibility (`deviceProtocolVersion`, `userConfigVersion`).
2. **Atomic Write Commitments:** Perform all flash memory and filesystem synchronizations as atomic transactions with write-verification readbacks.
3. **Macro Syntax Bounds Checking:** Reject macro scripts containing infinite loops, unbounded recursion, or unsafe timing parameters that could lock keyboard input.
4. **Bootloader Confirmation Gate:** Never trigger bootloader entry or firmware flash sequences without explicit confirmation and binary checksum validation.
5. **Zero Keystroke Logging:** Strictly prohibit capturing, logging, or exfiltrating real-time user keystroke telemetry outside of explicit macro debugging sessions.
