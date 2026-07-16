# 🔍 Reverse Engineering Challenge: `PatchMe2 - Revamped.exe`

## 📝 Overview
This repository details my solution to a 32/64-bit Windows crackme challenge (`PatchMe2 - Revamped.exe`). The objective was to suppress a sequence of intrusive "Nag" windows and reach the main application interface. 

By applying static analysis, control flow hijacking and binary patching, I successfully bypassed both the nag screens and the binary's underlying anti-tamper state machine.

## 💻 The relevant decompiled code was:

```c
    
void FUN_004011b0(void)

{
  HWND hWnd;
  
  hWnd = GetConsoleWindow();
  ShowWindow(hWnd,0);
  DAT_00404380 = 3;
  DAT_00404378 = 2;
  DAT_00404384 = 3;
  DAT_00404374 = "Welcome to Nag-O-mania 2009!";
  DAT_00404388 = "We Hope that You\'ll enjoy our software =) ";
  FUN_00401140(0x42,0x43);
  DAT_00404380 = DAT_00404380 + 1;
  if ((*(uint *)ProcessEnvironmentBlock & 0x10000) != 0) {
    DAT_00404378 = 0xd;
    DAT_00404380 = 0xd;
    DAT_00404384 = 0xd;
  }
  FUN_004014d0(DAT_00404374,DAT_00404388);
  FUN_004016a0();
  DAT_00404380 = DAT_00404380 + 1;
  if ((*(uint *)ProcessEnvironmentBlock & 0x10000) != 0) {
    DAT_00404378 = DAT_00404378 + DAT_00404380 / DAT_00404384;
    DAT_00404380 = DAT_00404380 / DAT_00404384 + DAT_00404378;
    DAT_00404384 = DAT_00404380 / DAT_00404384 + DAT_00404378;
  }
  DAT_0040437c = 3000;
  FUN_00401460("Balloon Nag of Death",3000);
  FUN_004016a0();
  DAT_00404380 = DAT_00404380 + 1;
  DAT_0040437c = 6000;
  if ((*(uint *)ProcessEnvironmentBlock & 0x10000) != 0) {
    DAT_00404378 = DAT_00404378 - DAT_00404384 * DAT_00404380;
    DAT_00404380 = DAT_00404378 - DAT_00404384 * DAT_00404380;
    DAT_00404384 = DAT_00404378 - DAT_00404384 * DAT_00404380;
  }
  FUN_004014d0("Nag-O-Mania would like to introduce...",
               "..It\'s Third Nag Window!! They just keep comming and comming =)");
  FUN_004016a0();
  DAT_00404380 = DAT_00404380 + 1;
  FUN_00401460("nag nag nag nag nag nag nag nag nag nag nag nag nag nag  ",DAT_0040437c);
  FUN_004016a0();
  DAT_00404380 = DAT_00404380 + 1;
  DAT_0040437c = 3000;
  if ((*(uint *)ProcessEnvironmentBlock & 0x10000) != 0) {
    DAT_00404378 = DAT_00404384 / DAT_00404378 + DAT_00404384 * DAT_00404380;
    DAT_00404380 = DAT_00404384 / DAT_00404378 + DAT_00404384 * DAT_00404380;
    DAT_00404384 = DAT_00404384 * DAT_00404380 + DAT_00404384 / DAT_00404378;
  }
  if ((DAT_00404378 == 6) && (DAT_00404384 == 6)) {
    DAT_00404380 = 0;
  }
  FUN_004014d0("This is the Main Window",
               "If you manage eliminate the nags before and after this window, congratulations! you did it!\n\tWrite a tutorial if you did it =) otherwise try again!"
              );
  if (DAT_00404380 != 0) {
    FUN_00401580();
  }
  return;
}


```
```c

void FUN_00401580(void)

{
  int iVar1;
  HMODULE hModule;
  FARPROC pFVar2;
  int iVar3;
  char *lpProcName;
  _NOTIFYICONDATAA local_1f4 [5];
  uint local_8;
  
  local_8 = DAT_00404000 ^ (uint)&stack0xfffffffc;
  lpProcName = "MessageBoxA";
  hModule = LoadLibraryA("User32.dll");
  pFVar2 = GetProcAddress(hModule,lpProcName);
  do {
    if ((*(uint *)ProcessEnvironmentBlock & 0x10000) != 0) {
      iVar1 = (DAT_00404384 * DAT_00404380) / 3;
      iVar3 = (int)(0x539 / (longlong)iVar1);
      DAT_00404380 = iVar3 + iVar1;
      DAT_00404384 = (DAT_00404384 * DAT_00404380) / 3 + iVar3;
    }
    (*pFVar2)(0,
              "Nag-O-Mania would like to inform you that someone is trying to remove it\'s nags o.0 how cruel are those people!\n\tre-Scan reports that nag-removal was attempted by you! locking program..."
              ,"Nag-Removal-Attempt Alert!",0);
    FUN_00401000(
                "Nag-O-Mania would like to inform you that someone is trying to remove it\'s nags o.0 how cruel are those people!\n\tre-Scan reports that nag-removal was attempted by you! locking program..."
                );
    Sleep(3000);
    Shell_NotifyIconA(2,local_1f4);
  } while( true );
}
```

## 🎯 The Challenge
The target executable is a compiled C/C++ Windows application. Upon execution, it attempts to exhaust the user by spawning multiple persistent Message Boxes (nags). 

**The Success State:** Reach the "Main Window" dialogue seamlessly without triggering the application's hidden nag-removal detection mechanisms.

## 💡 The Methodology
My initial attack vector was control flow hijacking. I patched the binary with an unconditional jump (`JMP`) prior to the nag sequence to branch directly to the Main Window execution block. 

**The Trap (Anti-Tampering):**
While the `JMP` successfully bypassed the nags, it caused the global counters to skip their required increments. Because the state variables never reached the required integer value of `6`, the validation check failed (`DAT_00404380 != 0`). Additionally, the PEB debugging checks actively corrupted the state variables during analysis. This unauthorized state automatically routed execution into `FUN_00401580`.

**The Penalty Function (`FUN_00401580`):**
This function is a deliberate punishment subroutine. It traps the user in an infinite `do...while(true)` loop, continuously spawn non-terminating `MessageBoxA` instances warning about a "Nag-Removal-Attempt Alert".

**The Final Solution:**
Instead of attempting to perfectly emulate the complex mathematical state of the global variables or NOP-ing every single PEB check, I attacked the penalty function directly. 

I navigated to the memory address of `FUN_00401580` and modified the prologue. By patching the very first instruction of the penalty function to a `RET` (Return, Opcode `0xC3`), the function immediately returns control to the caller as soon as it is invoked. 

**Patching Steps:**
1. **Initial Bypass:** Injected a `JMP` instruction to skip the initial nag rendering functions.
2. **Neutralizing the Trap:** Overwrote the first byte of `FUN_00401580` with `RET` .
3. **Result:** The binary detects the bypass, attempts to execute the infinite loop penalty, instantly returns, and safely halts at the successfully unlocked Main Window.

## 🚀 Usage
1. Clone this repository.
2. Run the executable in a Windows terminal (CMD or PowerShell):
   ```cmd
   .\PatchMe2 - Revamped.exe

