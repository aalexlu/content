# RISC-V Intro & Control Flow

## RISC-V Calling Conventions

**a0-a7, t0-t6, ra:** not guaranteed to be the same after a function call: 

- saved by caller before jumping to a function using jal

**sp, gp, tp, s0-s11:** guaranteed to be the same after a function call: 

## More

**a0-a7:** passed as arguments into functions

**a0, a1:** returned by functions

**sp:** stack pointer - moves down

**ra:** PC + 4 ; **rd:** current PC

**lw:** to ← : **sw:** from →

**j label / jal x0 label:** does not store ra

**ret:** jr ra

## Examples

If / else:

```
	addi s0, x0, 5 		//a
	addi s1, x0, 10		//b
	add t0, s0, s0		//t0 = a+a
	bne t0, s1, else
	xor s0, x0, x0		//a = 0
	jal x0, exit
else:
	addi s1, s0, -1		//b = a - 1
exit:
```

Array / looping:

```
	add t0, x0, x0		//t0 = 0 (loop index)
loop:
	slti t1, t0, 6		//if (t0 < 6) t1 = 1
	beq t1, x0, end		//loop while t0 < 6
	slli t2, t0, 2		//t2 = t0 * 4 (value to add for arr indexing)
	add t3, s0, t2		//t3 = s0 + t2 (new address to arr elem)
	lw t4, 0(t3)			//t4 = curr arr elem
	sub t4, x0, t4		//t4 = -t4
	sw t4, 0(t3)			//stores negated value
	addi t0, t0, 1
	jal x0, loop
end:
```

Full sumSquare function:

​	n^2+ (n−1)^2+ (n−2)^2+. . .+ 1^2

```
prologue:
	addi sp, sp, -12	//for s0, s1, ra
	sw ra, 0(sp)
	sw s1, 4(sp)
	sw s0, 8(sp)
sumSquare:
	addi s0, a0, x0		//need saved register, a0 is n passed in
	addi s1, x0, x0		//saved sum
loop:
	beq s0, x0, exit
	add a0, s0, x0		//a0 needed for call to square
	jal ra square			//ra ensures return to PC + 4
	add s1, s1, a0		//add to sum
	addi s0, s0, -1
	jal x0 loop
exit:
	add a0, s1, x0		//set a0 for callee
epilogue:
	lw ra, 0(sp)
	lw s1, 4(sp)
	lw s0, 8(sp)
	addi sp, sp, 12
	ret								//equivalent to ja ra (ra set by caller)
```

