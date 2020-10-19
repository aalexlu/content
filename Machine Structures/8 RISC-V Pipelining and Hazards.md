# RISC-V Pipelining and Hazards

## Pipelining Registers

Purpose of new registers: save values between stages; work that is done each stage

add +4 to the PC again in the memory stage because

save instruction in a register multiple times because



## Performance Analysis

|                  | Single Cycle | Pipelined  |
| ---------------- | ------------ | ---------- |
| fastest clk time | 950 ps       | 300 ps     |
| frequency        | 1.05 GHz     | 3.33 GHz   |
| latency          | 950 ps       | 1500 ps    |
| throughput       | 950 ps       | **300 ps** |

950/300 = 3.2x

- not 5x because adding clk-to-q / setup everytime (also hazards)

## Hazards

**Structural Hazards:** 

- Register File
- Memory

**Data Hazards:** data dependencies between instructions

- when an instruction reads a register before a previous instruction has finished writing to that register

**Control Hazards:** caused by jump and branch instructions

- PC is not PC + 4, but result is completed in EX stage

## Hazard Fixes

### Example 1

**Forwarding:** result of EX or MEM stage is sent to the EX stage for a following instruction to use

data hazard

| Instruction        | C1   | C2   | C3     | C4     | C5   | C6   | C7   | C8   |
| ------------------ | ---- | ---- | ------ | ------ | ---- | ---- | ---- | ---- |
| 1. addi t0, a0, -1 | IF   | ID   | **EX** | MEM    | WB   |      |      |      |
| 2. add s2, t0, a0  |      |      | IF     | **ID** | EX   | MEM  | WB   |      |
| 3. altiu a0, t0, 5 |      |      |        | IF     | ID   | EX   | MEM  | WB   |

*we know the value of a0 - 1 after EX and can then send to ID*

without forwarding

| Instruction        | C1   | C2   | C3   | C4   | C5   | C6   | C7   | C8   | C9   | C10  |
| ------------------ | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 1. addi t0, a0, -1 | IF   | ID   | EX   | MEM  | WB   |      |      |      |      |      |
| 2. add s2, t0, a0  |      | IF   | *    | *    | IF   | ID   | EX   | MEM  | WB   |      |
| 3. altiu a0, t0, 5 |      |      |      |      |      | IF   | ID   | EX   | MEM  | WB   |

### Example 2

**Forwarding and Stalling:**

| Instruction       | C1   | C2   | C3   | C4       | C5       | C6        | C7       | C8   | C9   |
| ----------------- | ---- | ---- | ---- | -------- | -------- | --------- | -------- | ---- | ---- |
| 1. addi s0, s0, 1 | IF   | ID   | EX   | MEM      | WB       |           |          |      |      |
| 2. addi t0, t0, 4 |      | IF   | ID   | **EX •** | MEM      | WB        |          |      |      |
| 3. lw t1, 0(t0)   |      |      | IF   | ID       | **• EX** | **MEM •** | WB       |      |      |
| 4. add t2, t1, x0 |      |      |      | *        | IF       | ID        | **• EX** | MEM  | WB   |

**Rearranging Code:**

| Instruction       | C1   | C2   | C3   | C4   | C5   | C6   | C7   | C8   | C9   |
| ----------------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 2. addi t0, t0, 4 | IF   | ID   | EX   | MEM  | WB   |      |      |      |      |
| 3. lw t1, 0(t0)   |      |      |      |      |      |      |      |      |      |
| 1. addi s0, s0, 1 |      |      |      |      |      |      |      |      |      |
| 4. add t2, t1, x0 |      |      |      |      |      |      |      |      |      |

