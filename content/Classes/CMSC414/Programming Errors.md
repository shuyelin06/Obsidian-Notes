---
title: Programming Errors
tags:
- cmsc414
---

This article broadly describes common security programming errors that occur, how to prevent them, as well as how to exploit them.

# Buffer Overflows
## Context: The Stack
In a simplified model, when we run a program, it is given a range of addresses. Let's say `MIN_ADDR` and `MAX_ADDR` are the minimum and maximum of this range. The heap will grow up from `MIN_ADDR`, and the stack will grow down from `MAX_ADDR`.
> `MIN_ADDR` | `HEAP` --> ... <-- `STACK` | `MAX_ADDR`

The stack is composed if a sequence of **frames**, which are created as functions call each other (here, the stack grows top down):
```mermaid
graph LR
1[Main Frame] -->
2[Func 1 Frame] -->
3[Func 2 Frame] -->
4[...]
```
> The "main" frame is the first frame created by entering our `main()` entrypoint to the program.

As functions call each other, more frames are added to the stack, and as functions return, these frames are popped off the stack.

Each of which has the following structure in memory (here, the stack grows left to right):
```mermaid
graph LR
1[Parameters] -->
2[Return Address] -->
3[Saved EBP] --> 4[ ] -->
5[Local Variables] --> 6[ ];

7[%esp] -.-> 4;
8[%ebp] -.-> 6;
```

The stack maintains 2 pointers in the current frame:
- The **Extended Stack Pointer (`%esp`)**, pointing to the current "top" of the stack (the lowest address of the current frame). 
- The **Extended Base Pointer (`%ebp`)**, pointing to the calling frame's EBP. Gives us a memory offset local to a function, which can be used to access parameters and variables. 

> For these namings, we will follow the nomenclature for 32-bit architectures.

## How Buffer Overflows Happen
Given the structure of the stack, we know that when we return from a function, we can use `%ebp + 4` to access the function's return address, and access the location of the next instruction of the program. 

But what if we overwrote this with another value? Let's say our current frame is
```mermaid
graph LR
1[char* str] -->
2[return addr] -->
3[saved EBP] -->
5["char a[10]"];
```
Then if we called `strcpy(a, str)`, where `str` is longer than 9 bytes, we could write past `char a[10]` and into the return address! This would cause the program to return to an overwritten address! This is an example of **buffer overflow**.
> Note that `strcpy` always adds `len(str) + 1`, due to the `NUL` byte at the end of the string.

We can take advantage of this to inject our own code! In the buffer write, we:
- Copy our own bytecode (called **shellcode**) to the overflowed buffer
- Overwrite the return address to the beginning of our bytecode

We can add our bytecode before or after the overwritten return address, depending on if the buffer can fit the entirety of our code. Here, the stack grows left to right.
```mermaid
graph LR
1[...] --> 2[new return] --> 3[shellcode];
4[shellcode] --> 5[new return] --> 6[garbage];
```
> In the first case, we simply fit all of our shellcode in the local variable memory. In the second case, we write garbage, and write our shellcode past the return address.

The second case will generally give us a lot more space to write our code to.

We could also similarly take advantage of this process to:
- Overwrite local variables
- Extract local variables (without having to modify the stack)
- Overwrite function parameters
- Extract function parameters (without having to modify the stack)
- Crash a program

## Preventing Buffer Overflow
### Assumptions and Bad Code
While we have to make assumptions about our programs, faulty assumptions will lead to vulnerabilities like buffer overflows. Even if they may have been correct before, changes in operating systems can suddenly make them incorrect!

If we have source code, we should check the following for buffer overflows:
- `strcpy()`
- `gets()` (especially in a loop)
- `memcpy()`
- `sprintf()`
- Array writes in loops

If we don't have source code, the following may indicate buffer overflow:
- Funny characters in output
- Segmentation faults
- Illegal instruction faults
- Repeated actions that should have the same result, but don't

Often, buffer overflows happen because programs read in user-controller data, which programmers mistakenly make assumptions about. While most users aren't malicious, not all of them aren't, and even normal users can also type in faulty imput.

To avoid buffer overflows, we should always assume that user input data is dirty, and adequately check it before using it. 
- Check input lengths
- Check for unexpected characters
- Check ranges for things like numbers
- Don't assume anything about the inputs

> [!Example] Example: Bad vs. Good Input Handling
> Do not call `printf(str)`, as `str` could contain format specifiers causing the function to look elsewhere in the stack for input (called a **format string vulnerability**). Instead, explicitly use a format specifier like `printf("%s", str)`.
> 
> Do not use `strcpy(dst, src)`, especially as we don't know how long `src` is. Instead, explicitly cap the amount of copying using `strncpy(dst, src, sizeof(dst))`.

> [!Info] Format String Vulnerabilities
> The previous example had an example of a **format string vulnerability**. In fact, `printf` has a signature `printf(format_string, ...)`, where the first argument tells the function what to expect next.
>
> If the format string has a format specifier (`%_`), they tell the function that there are additional function arguments to search for, making a naive `printf(str)` call dangerous (if we cannot guarantee what is in `str`).
> > If a format specifier is given without additional arguments, the function could search for and extract one of the local variables from the stack, which could expose data we don't want exposed.

### Preventing Buffer Overflows
To prevent buffer overflows, there are some techniques we can use!

In the **stack canaries** technique, we add special values to certain places of the stack and check if they change. If any of these values change, then we know something went wrong! 
> If these special values and locations are predictable, an attacker could still perform a buffer overflow and leave these values unchanged!

In the **non-executable stack** technique, we can mark parts of the stack to be non-executable, as it's almost always the case that an instruction pointer should not point to a stack location. This can prevent execution of shellcode on the stack.

In the **address randomization** technique, we can randomize where things are in memory every time a program is ran. This makes it a lot harder to exploit a vulnerability, as attackers won't be able to make assumptions about memory locations in the stack!
> **Address-Space Layout Randomization (ASLR)** randomizes where things are in memory every time you run.

### Defeating Buffer Overflow Protections
Here, we describe some ways we could (potentially) defeat the aforementioned protection techniques.

We could work around the **non-executable stack** technique using **return oriented programming (ROP)**, where we repeat the following:
1. **Groom** the stack, setting registers and arguments to useful values.
2. Set the instruction pointer to a **gadget**, which is existing library code with predictable addresses that use register values we've groomed, and ends with a return to take us to the next gadget. 
3. Repeat, repeatedly moving between gadgets to exploit our program. Eventually, we'll get code that's "functionally" the same as if we used shellcode!

> Note that our gadget doesn't need to be a normal function entrypoint! It could just be a few instructions that use register values that we've groomed.

---

We could also trick programs into running our own functions by exploiting environment variables! Most programs these days are **dynamically linked**, pulling important functions at load time from a variety of files (`.dll` files in windows). 

These files are found by searching a path, which can be controlled with the `LD_LIBRARY_PATH` environment variable. There is also a `LD_PRELOAD` environment variable which lets us load a dynamic library before anythig else. 
> Many people even have `.` in their executable path as the first entry, which is very dangerous!

We could exploit this to control the order where we search for libraries, having our own malicious programs be ran over standard programs instead!


# Vulnerabilities and Malware
## Properties of Secure Systems
We begin by discussing some rules that all secure systems should abide by. Unfortunately, not all systems abide by these rules, leading to vulnerabilities that can be exploited. 

The **principle of least privilege** states that any principal n a system should only have access to resources it needs for legitimate actions, and **absolutely nothing else**.

Commonly, this is implemented with **access control**, which is split into two categories:
- **Mandatory Access Control**: Controls that are mandated by the system.
- **Discretionary Access Control**: Optional controls that you can place in addition to mandatory controls.

Unfortunately, most software violates this principle of least privilege! 

Any secure system should also follow the **gold standard**, which has 3 working components:
- **Authentication**: Establishes the identity of a principal.
- **Authorization**: Establishes the permissions of an identity. Includes access control.
- **Auditability**: Ensures that all operations can be inspected / validated later. Commonly done with logs that store actions.

## Vulnerability Equities
Finding and fixing vulnerabilities is often not easy. While there are people who try want to find these vulnerabilities to fix them, there are also people who want to find these vulnerabilities to exploit them. 

This leads to the **equities problem**. People who find vulnerabilities essentially have found "equity" in the system, and may not share these vulnerabilities to be fixed, as its not as profitable for them to do so. Instead, it may actually be more worth it to share them to be exploited instead.


## Malware
**Malware** is any malicious software that runs on a victim's system. 

### Categories of Malware
There are 3 general categories of malware, described below.

**Viruses** are malware that hide in executable parts of files, that try to evade detection by security programs. They are ran when this executable part is ran, and propagate based on user actions (that prompt the execution of the stored code).

**Worms** are malware that hide in running code behind the scene, that (generally) try to hide themselves from programs that can find them. They tend to propagate automatically, and try to spread rapidly.

**Trojans** are malware that immitate legitimate software, but do more than the user believes. They tend to be propagated by the attacker, who delivers the software.

> In more recent years, malware has begun to blend between these categories.

### Infection Vectors
An **infection vector** is a component that malware can used to gain access into a system. There are some common vectors, including:
- **Vulnerable Network Services**: Services on a network which are vulnerable, commonly to buffer overflows. 
- **Backdoor Logins**: Components that are left by developers to leave a way into the system. Sometimes this is dont by laziness rather than malice.
- **Social Engineering**: Attempts to persuade people to give up information into a system, or run an executable to grant access.
- **Trojan Horse**: A trojan malware that can grant other malwares access.
- **Physical Access**: Physical peripheral hardware with the malware, or unsecured network ports or terminals that people can access.

### Effects
The effects of malware depend primarily on the goals of the creator, and what they want to do with the malware. Some common goals include:
- System disruption
- Defacement of a publicly visible service
- Destruction of data
- Crashing of a system
- Stealing data (otherwise known as **data exfiltration**)
- Send spam
- Extort money from victims
- Rootkits for later access
