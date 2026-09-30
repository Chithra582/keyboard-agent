# Agent Explainability & Transparency Report

- **Agent Name:** uhk-keyboard-agent
- **OpenGAP Specification:** 0.1.0
- **Agent ID:** uhk-keyboard-agent
- **Domain:** Developer Tools / Hardware Peripheral Configuration & Smart Macro Runtime
- **Passport Validation Tier:** Tier-1 Certified Autonomous Agent

---

## 1. Overview & Architectural Purpose

The **Ultimate Hacking Keyboard Agent** (`uhk-keyboard-agent`) is a dedicated hardware-interfacing autonomous agent designed to configure, program, and maintain Ultimate Hacking Keyboard hardware peripherals and modular attachments. Leveraging a robust multi-package architecture—spanning `uhk-agent`, `uhk-usb`, `uhk-fs`, `uhk-smart-macro`, `kboot`, and `mcumgr`—the agent automates hardware communication over USB HID, validates and compiles smart macro domain-specific language (DSL) routines, synchronizes internal EEPROM flash layouts, and executes fail-safe firmware updates.

Designed to eliminate hardware misconfiguration risks, the agent validates every operation deterministically before committing changes to physical flash memory.

---

## 2. How the Agent Decides (Decision-Making Logic)

### 2.1 Hardware Discovery & USB Protocol Handshake
- **Decision:** Determines device identity, attached hardware modules (trackball, trackpoint, touchpad, key cluster), and protocol versions.
- **Rules:**
  - Scans system USB HID endpoints matching vendor ID (`0x1D50`) and product identifiers.
  - Queries device firmware version, protocol revision, and hardware generation (UHK 60 v1 vs. v2).
  - Enforces backward compatibility fallbacks if device protocol mismatches the host agent capability.

### 2.2 Smart Macro Compilation & AST Validation
- **Decision:** Analyzes user-defined smart macro scripts and compiles them into validated on-device bytecode.
- **Rules:**
  - Tokenizes and parses macro DSL scripts against language grammar rules (`if`, `holdKey`, `delay`, `pressKey`).
  - Checks timing parameters against hardware rate limits to prevent buffer saturation on the embedded MCU.
  - Rejects cyclic dependencies, unclosed blocks, or ambiguous modifier key combinations prior to packaging.

### 2.3 EEPROM Filesystem Synchronization & Wear Leveling
- **Decision:** Determines optimal binary serialization and sector write routines for the on-device flash filesystem (`uhk-fs`).
- **Rules:**
  - Computes differential hashes between host configuration state and device EEPROM contents.
  - Skips rewriting unmodified memory blocks to extend flash memory lifespan and minimize wear.
  - Executes atomic commit markers to guarantee that interrupted transfers do not leave the device in an inconsistent state.

### 2.4 Firmware Integrity Check & Safe Bootloader Transition
- **Decision:** Evaluates target firmware binary compatibility and orchestrates bootloader upgrades (`kboot` / `mcumgr`).
- **Rules:**
  - Computes SHA-256 cryptographic hashes and verifies cryptographic signatures against official release catalogs.
  - Confirms hardware platform revision matches target binary before initiating reboot into bootloader mode.
  - Holds recovery bootloader states open with retry protocols to safely resume in case of bus disconnects.

---

## 3. Data Sources & Inputs Used

| Data Input | Source | Purpose | Data Handling & Privacy |
| :--- | :--- | :--- | :--- |
| USB HID Device Descriptors | Connected physical UHK hardware | Identifies keyboard model, firmware, and modules | Ephemeral runtime query, strictly local |
| Keymap Configurations & Profiles | Local user configuration files (`uhk-web`) | Defines key mappings, layer layouts, and shortcuts | Stored locally on disk and device flash |
| Smart Macro Script Files | User-authored macro DSL scripts | Automates complex keystroke sequences | Validated in memory without external transmission |
| Firmware Release Binaries | Official UHK GitHub repository / local assets | Updates embedded microcontroller firmware | Checksum verified, cached locally |

---

## 4. Known Limitations & Failure Modes

1. **USB Bus Disconnection During Flashing:**
   - *Limitation:* Physical cable disconnect during bootloader flash writing can interrupt image transmission.
   - *Mitigation:* Bootloader recovery mode (`kboot`/`mcumgr`) remains resident in protected ROM to allow re-flashing.

2. **OS-Level USB Permission Restrictions:**
   - *Limitation:* Linux `udev` rules or Windows driver issues may block raw HID access without root/administrator privileges.
   - *Mitigation:* Automated permission detection and actionable guidance for `udev` rules configuration.

3. **Macro Timing Incompatibilities:**
   - *Limitation:* Overly aggressive delays or rapid keystrokes may cause missed inputs on target operating systems.
   - *Mitigation:* Conservative default delays and built-in AST timing bounds checking.

4. **Flash Storage Exhaustion:**
   - *Limitation:* Highly complex multi-layer configurations with extensive macros may exceed EEPROM space limits.
   - *Mitigation:* Pre-compilation byte count estimation and proactive warning before sector allocation.

---

## 5. Verification, Safety & Human Oversight

- **Zero Unprompted Flash Operations:** Writing to EEPROM or triggering bootloader mode always requires explicit user confirmation.
- **Differential Diff Preview:** Visualizes changes between active hardware layout and proposed modifications prior to write execution.
- **Non-Destructive Read-Only Querying:** Diagnostic commands and state queries are strictly read-only and cannot alter keyboard functionality.
- **Hardware Fallback Keystrokes:** Firmware supports hardcoded hardware recovery key combinations to re-enter bootloader independently of host software.
