# OS, VM Notes

## Lecture 28 Intro

#### OS at Boot

1. Basic Input Output System (BIOS): find a storage device and load first sector (block of data)
2. Bootloader: load the OS *kernel* from a disk into a location in memory and jump into it
3. Init: launch an application that waits for input in loop
4. OS Boot: initialize services, drivers, etc.

#### Superviser Mode

* (to protect the OS from the application)*
* process can only access a subset of instructions and memory when not in supervisor mode

#### Interrupts, Exceptions

- **Interrupt:** something <u>external</u> to the running program
- **Exception:** something done <u>by the running program</u>
  - ex 5-stage pipeline: PC address exception, illegal opcode, data address exceptions
- ECALL: trigger an exception to the <u>higher</u> privilege
- EBREAK: trigger an exception within the <u>current</u> privilege
- **Trap:** act of servicing an interrupt or exception by hardware jump
  - trap handling: exceptions are handled *like pipeline hazards*

## Lecture 29

#### Storage Disk

- attached as peripheral I/O device
  - SSD (solid state drive) - faster no moving parts
  - HDD (hard disk drive) - slower moving parts

#### Memory Manager

1. Map virtual to physical addresses
2. Protection *(isolation)*
3. Swap memory to disk *(illusion)*

paged memory: physical memory (DRAM) broken into pages

page faults

## Lecture 30

Impact of Paging on AMAT

