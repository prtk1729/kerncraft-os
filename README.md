# Kerncraft OS

A 32-bit multitasking operating system and kernel developed entirely from scratch as part of a systems programming project during my time at college. Built in low-level C and x86 assembly, this OS features a real mode bootloader, memory management, task scheduling, FAT16 filesystem support, ELF binary loading, and a basic shell.

---

## 🚀 Features

- 🧠 **Custom Kernel** – Designed from the ground up with memory protection, paging, and context switching.
- 🧰 **Bootloader in Assembly** – Real-mode bootloader outputs to screen, loads the kernel from disk.
- 💾 **FAT16 Filesystem Support** – Reads files and parses FAT tables manually.
- 🧱 **Memory Virtualization** – Implements paging and address translation for user/kernel space isolation.
- 🧮 **Custom Heap** – `malloc()` and `free()` functionality through a self-managed dynamic memory allocator.
- 🗃️ **ELF Binary Loader** – Supports loading of ELF executables into protected memory.
- 🎹 **Keyboard Driver** – Interrupt-based input handling using PS/2 keyboard scancode parsing.
- 🧵 **Multitasking Support** – Preemptive multitasking with task scheduling and context switching.
- 💻 **Interactive Shell** – Simple shell interface for running programs and interacting with the OS.
- 🐞 **Debuggable with GDB** – Run and debug using QEMU + GDB.

---

## 🧑‍💻 Development Overview

### Architecture:
- **Language:** C (for the kernel), x86 Assembly (for bootloader and low-level interfaces)
- **Target:** x86 (Intel 32-bit protected mode)
- **File System:** FAT16
- **Executable Format:** ELF (32-bit)

### Components:
| Module               | Description                                               |
|----------------------|-----------------------------------------------------------|
| Bootloader           | Real-mode stage written in pure x86 assembly              |
| Kernel Loader        | Switches to protected mode and sets up GDT & paging       |
| Virtual Memory       | Paging, address mapping, protection rings                 |
| File System          | FAT16 sector reading, cluster chaining, file access       |
| ELF Loader           | Loads and parses ELF headers for program execution        |
| Process Manager      | Implements task structs, state transitions, scheduling    |
| Input Handling       | Keyboard driver with interrupt-based scancode decoding    |
| Heap Allocator       | Custom malloc/free for dynamic memory in kernel space     |
| Shell                | Basic command-line interpreter to run kernel tasks        |

---

## 🔧 Building and Running

### Prerequisites:
- GCC cross-compiler (`i686-elf-gcc`)
- NASM
- QEMU
- Make
- Ubuntu (preferred)

### Setup:
```bash
sudo apt update
sudo apt install build-essential nasm qemu qemu-system make
```

