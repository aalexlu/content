# Logic, SDS, FSM

## Boolean Logic

| Name         |          AND Form          |          OR Form           |
| ------------ | :------------------------: | :------------------------: |
| Commutative  |          AB = BA           |       A + B = B + A        |
| Associative  |       AB(C) = A(BC)        | A + (B + C) = (A + B) + C  |
| Identity     |           1A = A           |         0 + A = A          |
| Null         |           0A = 0           |         1 + A = 1          |
| Absorption   |        A(A + B) = A        |         A + AB = A         |
| Distributive |  (A + B)(A + C) = A + BC   |     A(B + C) = AB + AC     |
| Idempotent   |          A(A) = A          |         A + A = A          |
| Inverse      |          A(Ā) = 0          |         A + Ā = 1          |
| De Morgan's  | (<u>AB</u>) = Ā + <u>B</u> | <u>A + B</u> = Ā(<u>B</u>) |

Example 1 (De Morgan's):

````
!A + AB
!A + !(!(AB))
!(A(!(AB)))
!(A!A + !B))
!(A!A + A!B)
!(A!B)
!A + B
````

Example 2:

````
(A + B)(A + not(B))C
(AA + Anot(B) + AB + Bnot(B))C
(A + A(not(B) + B) + 0)
AC
````

*view worksheet*

## Logic Gates

| not  | and  | or   | xor  | nand | nor  | xnor |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| \|>o | \|>  | )>   | ))>  | \|>o | )>o  | ))>o |

**Gates to Boolean:** 

| A    | B    | NAND(A, B) | XOR(A, B) | XNOR(A, B) |      |
| ---- | ---- | ---------- | --------- | ---------- | ---- |
| 0    | 0    | 1          | 0         | 1          | !A!B |
| 0    | 1    | 1          | 1         | 0          | !AB  |
| 1    | 0    | 1          | 1         | 0          | A!B  |
| 1    | 1    | 0          | 0         | 1          | AB   |

**NAND to Boolean: **(!A!B + !AB + A!B) or (!(AB) = !A + !B)

**XOR to Boolean:** (!AB + A!B)

**XNOR to Boolean:** (!A!B + AB)

Create AND from NANDs

- NAND-NOT→AND
- *NOT(A) = NAND(A, A)*
- NAND(A, B)-NAND(A, A)→AND

## State Design System

**state elements:** keeps state / keeps memory of previous signals - change based on clock signal

**clock (clk):** heartbeat of system; keeps track of timing; keeps everything in sync

**flip-flop:** state element that holds 1 bit -> 32 bit reg := 32 connected flip flops

**register:** n-bit state element used to hold all types of values

**set-up time:** amount of time <u>before</u> rising clock edge that the input has to stay stable for

**hold time:** amount of time <u>after</u> rising clock edge that the input has to stay stable for for

**clk-to-q:** amount of time <u>after</u> rising clock edge until register's input is reflected on output

**critical path:** clk-to-q + max CL block + set-up time

- (reg1) (amt of delay) (reg2)
- <u>min. clk period</u> = critical path time
- <u>max clk frequency</u> (cycles / s) = 1 / (min. clk period)

**max hold time:** clk-to-q (from prev register) + shortest CL

**Other**

Simplifying boolean logic expressions optimize gates: reduced gates; performance up

Speed of circuit: depends on parallel / series setup

**Problems:** line by line draw waves - *view hw05, disc*

## Finite State Machine

**next state and output** depend on **current state and input**

0/1 - input/output(input to next)

**Examples:**

- pattern in a bitstring - move through states
- repeating recent bits - having start, last bit 0, and last bit 1 states
- regex pattern - start, pattern begin, pattern hasn't begun states