# ReverseEngineering

## About

This repository contains a collection of reverse engineering challenges and crackmes that I have analyzed, solved, or created to practice and improve my binary analysis skills. Rather than just storing the code, each project folder contains its own documentation explaining the challenge logic, decompiled code and the required inputs to solve them.

The objective of this repository is to build a structured portfolio of reverse engineering projects while continuously improving my understanding of assembly, C programming, and software execution flow.

---

## Repository Structure

```text
ReverseEngineering/
├── crackmes/
│   └── RE7/
│   └── patchme2_revamped/
└── README.md
```

## Projects

| Project | Difficulty | Type | Summary |
| :--- | :---: | :---: | :--- |
| [RE7](./crackmes/RE7/) | 🟢 Beginner | Crackme | A basic logic challenge that requires passing two conditional checks by converting hardcoded hexadecimal values (`0x21` and `0x66`) to their decimal equivalents (33 and 102). |
| [patchme2_revamped](./crackmes/patchme2_revamped/) |  🟡 Intermediate | Crackme | Defeated PEB anti-debug checks and state-machine validation by hijacking control flow (`JMP`) and neutralizing the penalty trap (`RET`). |


---

## Concepts Covered

* **Static Analysis:** Reading and understanding decompiled C code.
* **Data Representation:** Converting between Hexadecimal and Decimal numeral systems.
* **Control Flow:** Analyzing `if` statements and conditional jumps to find the execution path to the success message.
* **Basic Input/Output:** Understanding how `scanf` and `printf` handle user interaction and variable assignment in C.
* **Binary Patching:** Modifying compiled code by injecting assembly opcodes (`JMP`, `RET`) to alter program behavior.
* **Anti-Debugging Evasion:** Identifying checks (like reading the PEB) meant to detect debuggers and analysis tools.
* **State Machine Analysis:** Analyzing global variables used as hidden execution counters to validate program flow.
* **Function Neutralization:** Disarming penalty functions by patching the prologue with an early return.

---

## Tools & Libraries

* C Programming
* Decompilers / Disassemblers (Ghidra, IDA Pro)
* GNU Compiler Collection (GCC)
* Git & GitHub
