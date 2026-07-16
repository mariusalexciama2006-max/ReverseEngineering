\# 🕵️‍♂️ Crackme Solution: code.exe (No Ghidra Required)



\## 📝 Overview

This repository contains my solution to a straightforward reverse-engineering challenge (`code.exe`). The binary was simple enough that it didn't require decompilation suites like Ghidra or IDA Pro. Sometimes, keeping it simple is the most efficient way to get the flag.



\## 🎯 The Challenge

The target is a 64-bit Windows console application (compiled with MinGW-w64). Upon execution, the program prompts the user for two inputs:

1\. `Enter Your Number :` 

2\. `Enter The Secret Key :` 



Providing the correct combination triggers the success message: 

> \*"Congratulations, you have completed the challenge!"\*



\## 💡 The Solution

Because the binary isn't heavily obfuscated or packed, I bypassed the need for advanced static analysis. 



\*\*My approach:\*\* \*I dumped the binary's strings and located the win condition in the `.rdata` section. Adjacent to the success string, I identified a hardcoded hex value. By converting this hex to decimal, I immediately recovered the expected inputs.\*



\*\*The Winning Inputs:\*\*

\* \*\*Number:\*\* `\[Insert the winning number]`

\* \*\*Secret Key:\*\* `\[Insert the winning key]`



\## 🚀 How to Run

1\. Clone this repository.

2\. Open a terminal (Command Prompt or PowerShell).

3\. Execute the binary:

&#x20;  ```cmd

&#x20;  .\\code.exe

