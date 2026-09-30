---
name: "smart-macro-dsl-compiler"
description: "Validates, parses, and compiles UHK smart macro DSL scripts into on-device execution bytecode."
---

# Smart Macro DSL Compiler Skill

## Overview
Compiles high-level macro scripts into deterministic bytecode executable by the UHK microcontroller:
- Parses syntax for conditional blocks, key holds, sequences, and layer switches.
- Validates timing bounds to prevent USB HID buffer overflows or OS lockups.
- Emits compact binary representations optimized for embedded flash memory.

## Capabilities
- Abstract Syntax Tree (AST) validation and error localization.
- Macro execution simulation to detect potential deadlocks.
- Optimization of redundant delay instructions.
