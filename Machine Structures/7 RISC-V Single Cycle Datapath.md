# RISC-V Single Cycle Datapath

|      | Stage              |                                                              |
| ---- | ------------------ | ------------------------------------------------------------ |
| IF   | Instruction Fetch  | **PC** and **IMEM** (gives 32 bit instruction)               |
| ID   | Instruction Decode | **RegFile** (split into register fields) and **Immediate Generator** (gives imm) |
| EX   | Execute            | **MUXes** (chooses operands) and **ALU** (operation stage) and **Branch Compator** (determines if we want to branch) |
| MEM  | Memory             | **DMEM** (holds all of our non instruction data - used for loads and stores) |
| WB   | Write Back         | Wire back to RegFile (writing back to the rd - for jump and links / arithmetic / load words) |

## ---VIEW DIAGRAM---

| PCSel                                                        | inst | RegWEn                                   | ImmSel | BrEq | BrLt | BSel                                     | ASel                                    | ALUSel              | MemRW                                           | WBSel                                                       |
| ------------------------------------------------------------ | ---- | ---------------------------------------- | ------ | ---- | ---- | ---------------------------------------- | --------------------------------------- | ------------------- | ----------------------------------------------- | ----------------------------------------------------------- |
| 0→PC+4, 1→ALU (for jumps, branches) decided by result of ALU |      | whether we want to write back at the end |        |      |      | if need to operate on imm instead of rs2 | if need to operate on PC instead of rs1 | 0→add, 1→sub, 2→mul | will get write data - but may not want to write | what will be written back to rd - 0→PC+4, 1→ALU, 2→mem (lw) |
| EX                                                           | IF   | ID                                       | ID     | EX   | EX   | EX                                       | EX                                      | EX                  | MEM                                             | WB                                                          |

**Single Cycle Datapath:**

- does **not** make use of all hardware units for each instruction
  - but every instruction does go through every component (even if meaningless)
- cannot execute its stages in parallel: values in later stages depend on computations in earlier ones
- combinational logic everywhere

## Control Signals

|      |      | BrEq | BrLT | PCSel    | ImmSel | BrUn | ASel    | BSel    | ALUSel | MemRW | RegWEn | WBSel   |
| ---- | ---- | ---- | ---- | -------- | ------ | ---- | ------- | ------- | ------ | ----- | ------ | ------- |
| R    | add  | *    | *    | 0 (PC+4) | *      | *    | 0 (rs1) | 0 (rs2) | add    | 0     | 1      | 1 (ALU) |
| I    | ori  | *    | *    | 0 (PC+4) | I      | *    | 0 (rs1) | 1 (imm) | or     | 0     | 1      | 1 (ALU) |
| I    | lw   | *    | *    | 0 (PC+4) | I      | *    | 0 (rs1) | 1 (imm) | add    | 0     | 1      | 2 (mem) |
| S    | sw   | *    | *    | 0 (PC+4) | S      | *    | 0 (rs1) | 1 (imm) | add    | 1     | 0      | *       |
| B    | beq  | 0/1  | *    | 0/1      | SB     | *    | 1 (PC)  | 1 (imm) | add    | 0     | 0      | *       |
| J    | jal  | *    | *    | 1 (ALU)  | UJ     | *    | 1 (PC)  | 1 (imm) | add    | 0     | 1      | 0       |
| B    | bltu | *    | 0/1  | 1/0      | SB     | 1    | 1 (PC)  | 1 (imm) | add    | 0     | 0      | *       |

## Clocking Methodology

**state element:** element connected to the clock

- <u>input signal</u> to each state element must stabilize before <u>rising edge</u>

**critical path:** longest delay path between state elements in circuit

- clk-to-q + max CL block + set-up time
- circuit cannot be clocked faster than this
- placing registers in critical path <u>reduces the amount of logic between registers</u>

**clk frequency:** 1 / cycle time

Stages of the datapath that instructions use:

|      | IF: 200ps | ID: 100ps | EX: 200ps | MEM: 200ps | WB: 100ps | Total Time |
| ---- | :-------: | :-------: | :-------: | :--------: | :-------: | :--------: |
| add  |     √     |     √     |     √     |            |     √     |   600ps    |
| ori  |     √     |     √     |     √     |            |     √     |   600ps    |
| lw   |     √     |     √     |     √     |     √      |     √     |   800ps    |
| sw   |     √     |     √     |     √     |     √      |           |   700ps    |
| beq  |     √     |     √     |     √     |            |           |   500ps    |
| jal  |     √     |     √     |     √     |            |     √     |   600ps    |
| bltu |     √     |     √     |     √     |            |           |   500ps    |

critical path - lw

fastest you can clock this single cycle datapath

- 1 / 800 ps
- 1 / (800 * 10^-12) seconds
- 1,250,000,000  s^-1
- 1.25 GHz

inefficient since based on slowest instruction and there are idle resources

→ pipelining!

