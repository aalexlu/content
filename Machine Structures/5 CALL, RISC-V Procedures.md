 # CALL, RISC-V Procedures

## CALL stack diagram

|                      CALL stack diagram                      |
| :----------------------------------------------------------: |
|                       C program: foo.c                       |
| **Compiler** - compiles from C to assembly (can incl. pseudo) |
|                   Assembly program: foo.a                    |
| **Assembler** - split la,li; labels replaced so offsets to absolute addresses; everything absolute |
|                      Object Code: foo.o                      |
| **Linker** ← lib.o - resolves / relocates absolute file addresses |
|             Executable a.out (Machine Language)              |
|          **Loader** - loading executable to memory           |
|                            Memory                            |

## CALL

**Stored Program concept:** instructions are data are bits; programs can manipulate other progs w/o changing hardware

**Assembler:** makes 2 passes through code

1. store labels / values in symbol table + replace non-forward references
2. resolve <u>forward referencing</u> (using label before defining)

**Object Files:** outputted by Assembler - 6 main parts

- Header - size, #, positions of other parts
- Text - code itself
- Data - binary representation of data in src file (directives constants)
- Relocation Table - IDs lines linker needs (absolute referencing)
- Symbol Table - list of labels (function data) that are referenced
- Debugging Information - 

## RISC-V Addressing

**Addressing Modes** to access memory

1. Base displacement - 
2. PC-relative - 
3. Register - 

12 bits /2 =