 # CALL, RISC-V Procedures

## CALL stack diagram

|                      CALL stack diagram                      |
| :----------------------------------------------------------: |
|                       C program: foo.c                       |
| **Compiler** - compiles from C to assembly (can output pseudo) |
|                   Assembly program: foo.a                    |
| **Assembler** - replaces pseudo; labels replaced so offsets to absolute addresses; everything absolute |
|                      Object Code: foo.o                      |
| **Linker** ← lib.o - resolves / relocates absolute file addresses |
|             Executable a.out (Machine Language)              |
|          **Loader** - loading executable to memory           |
|                            Memory                            |

## CALL

**Stored Program concept:** instructions are data are bits; programs can manipulate other progs w/o changing hardware

**Assembler:** makes 2 passes through code; to object code *(resolves relative addressing)*

1. store labels / values in symbol table + replace non-forward references
2. resolve <u>forward referencing</u> (for jumps using label before defining)

ex: la split to auipc, addi

**Object Files:** outputted by Assembler - 6 main parts (already mostly binary)

- Header - size, positions of other parts (for linker)
- Text - machine code itself
- Data - binary representation of data in src file (directives constants)
- Relocation Table - lines of codes that the linker needs (external and static; absolute referencing)
- Symbol Table - list of labels (function data) that are referenced
- Debugging Information - additional info for debuggers (flags)

**Linker:** also responsible for inserting external code from lib.o *(resolves absolute addressing)*

## RISC-V Addressing

**Addressing Modes** to access memory

1. Base displacement - adds an immediate to a register value to create a memory address (lw, lb, sw, sb)
2. PC-relative - uses PC and adds the immediate value of the instruction (*2) to create an address (used by branch and jump instructions)
   - range of 32-bit instructions that can be reached: 12 bits for immediate (signed)
     - PC + (2 * immediate) = 2 * [-2^11, 2^11-1]
     - [-2^12, 2^12-2]
     - 4 byte instructions: [-2^10, 2^10-1]
3. Register - uses the value in a register as a memory address (jalr, jr, ret)
   - range of 32-bit instructions that can be reached: 20 bits for immediate (signed)
     - PC + (2 * immediate) = 2 * [-2^19, 2^19-1]
     - jump: [-2^20, 2^20-2]
     - 4 byte instructions: [-2^18, 2^18-1] 

**Examples**

``````
0x002cff00:	loop:	add t1, t2, t0
0x002cff04:				jal ra, foo
0x002cff08:				bne t1, zero, loop
...
0x002cff2c:	foo:	jr ra
``````

```add t1, t2, t0```

| funct7  | rs2 (x5) | rs1 (x7) | funct3   | rd (x6) | opcode  |
| ------- | -------- | -------- | -------- | ------- | ------- |
| 0000000 | 00101    | 00111    | 000      | 00110   | 0110011 |
| 31 - 25 | 24 - 20  | 19 - 15  | 14  - 12 | 11 - 7  | 6 - 0   |
| 0x00    | 5        | 38       |          | 33      | 3       |

```jal ra, foo```

| imm[20\|10:1\|11\|19:12] (2c-04) (no imm[0]) | rd (x1) | opcode  |
| -------------------------------------------- | ------- | ------- |
| 0 000010100 0 00000000                       | 00001   | 1101111 |
| 31 - 12                                      | 11 - 7  | 6 - 0   |
| 0x02800                                      | 0e      | f       |

```bne t1, zero, loop```

| imm[12\|10:5] | rs2 (x0) | rs1 (x6) | funct3  | imm[4:1\|11] | opcode  |
| ------------- | -------- | -------- | ------- | ------------ | ------- |
| 1 111111      | 00000    | 00110    | 001     | 1100 1       | 1100011 |
| 31 - 25       | 24 - 20  | 19 - 15  | 14 - 12 | 11 - 7       | 6 - 0   |
| 0xfe          | 0        | 31       |         | ce           | 3       |

```ja ra```

jal stores PC + 4 into ra

ra = 0x002cff04 + 4 = 0x002cff08