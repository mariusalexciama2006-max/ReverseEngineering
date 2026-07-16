# ReverseEngineering

## About

This repository contains a collection of reverse engineering challenges and crackmes that I have analyzed, solved, or created to practice and improve my binary analysis skills. Rather than just storing the code, each project folder contains its own documentation explaining the challenge logic, decompiled code snippets, and the required inputs to solve them.

The objective of this repository is to build a structured portfolio of reverse engineering projects while continuously improving my understanding of assembly, C programming, and software execution flow.

---

## Repository Structure

```text
ReverseEngineering/
├── crackmes/
│   └── RE7/
└── README.md
```

## Projects

| Project | Difficulty | Type | Summary |
| :--- | :---: | :---: | :--- |
| [RE7](./crackmes/RE7/) | 🟢 Beginner | Crackme | A basic logic challenge that requires passing two conditional checks by converting hardcoded hexadecimal values (`0x21` and `0x66`) to their decimal equivalents (33 and 102). |

---

## Concepts Covered

* **Static Analysis:** Reading and understanding decompiled C code.
* **Data Representation:** Converting between Hexadecimal and Decimal numeral systems.
* **Control Flow:** Analyzing `if` statements and conditional jumps to find the execution path to the success message.
* **Basic Input/Output:** Understanding how `scanf` and `printf` handle user interaction and variable assignment in C.

---

## Tools & Libraries

* C Programming
* Decompilers / Disassemblers (Ghidra, IDA Pro)
* GNU Compiler Collection (GCC)
* Git & GitHub
