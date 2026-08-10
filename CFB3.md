# WRITE UP: [RE] CrackNotMe's CrackmesForBeginners (CFB) #3
**Difficulty:** 2.0  
**Quality:** 4.5  

## Challenge Overview

<img width="1247" height="334" alt="image" src="https://github.com/user-attachments/assets/736910e4-3b51-493d-8864-51022ef21378" />

you can find this challenge in [here](https://crackmes.one/crackme/6a154aca8fab7bbca27302a2).

### Description

This is the third challenge from the Crackmes for Beginners (CFB) series.
Welcome to the realm of custom code virtualization! Standard high-level decompilers won't show you the validation math in the control flow graph. Instead, the binary executes a custom 120-byte bytecode program using a built-in micro-virtual machine.
To solve this challenge, you'll need to analyze the interpreter loop, map out the 9 custom 3-byte instructions, write a simple disassembler, and reverse-engineer the bytecode to reconstruct the correct activation password.

---

## Information Gathering & Static Analysis

After loading the file into Ghidra, I started at the `entry` point, which led me to the C Runtime (CRT) initialization function: `__scrt_common_main_seh()`. 

By scrolling down to the bottom of this CRT function, I found the call to the actual `main` function (which takes 3 parameters: `argc`, `argv`, `envp`) right before the `_cexit()` call. Ghidra named it `FUN_1400034a0`.

```C
// Inside __scrt_common_main_seh()
uVar6 = FUN_1400034a0(*puVar10,uVar1,uVar8); // This is the real main()
```

