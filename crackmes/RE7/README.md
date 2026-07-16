# 🔍 Reverse Engineering Challenge: `code.exe`

## 📝 Overview
This repository details my solution to a 64-bit Windows crackme challenge (`code.exe`). By applying lightweight static analysis and pattern matching, I successfully extracted the required inputs to solve the challenge without needing heavy decompilers like Ghidra or IDA Pro.

## 🎯 The Challenge
The target executable is a console application compiled with MinGW-w64. Upon execution, it requires two specific inputs to unlock the success state:
1. `Enter Your Number :` 
2. `Enter The Secret Key :` 

Providing the correct combination triggers the target flag: 
> *"Congratulations, you have completed the challenge!"*

## 💡 The Methodology
Rather than jumping straight into a disassembler, I leveraged surface-level static analysis to trace the program's logic. 

**How I solved it:** *I dumped the binary's strings and located the win condition in the `.rdata` section. Adjacent to the success string, I identified a hardcoded hex value. By converting this hex to decimal, I immediately recovered the expected inputs.*

**The Solution:**
* **Target Number:** `[Insert Number]`
* **Secret Key:** `[Insert Key]`

## 🚀 Usage
1. Clone this repository.
2. Run the executable in a Windows terminal (CMD or PowerShell):
   ```cmd
   .\code.exe
