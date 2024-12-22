# Reverse Engineering  

## ARMssembly 1  
<img width="433" alt="image" src="https://github.com/user-attachments/assets/fb4cee2d-3a76-4ac5-86dc-5bd05f29d20f" />  

The program is of assembly language.  
```
 .arch armv8-a
	.file	"chall_1.c"
	.text
	.align	2
	.global	func
	.type	func, %function
func:
	sub	sp, sp, #32
	str	w0, [sp, 12]
	mov	w0, 81
	str	w0, [sp, 16]
	str	wzr, [sp, 20]
	mov	w0, 3
	str	w0, [sp, 24]
	ldr	w0, [sp, 20]
	ldr	w1, [sp, 16]
	lsl	w0, w1, w0
	str	w0, [sp, 28]
	ldr	w1, [sp, 28]
	ldr	w0, [sp, 24]
	sdiv	w0, w1, w0
	str	w0, [sp, 28]
	ldr	w1, [sp, 28]
	ldr	w0, [sp, 12]
	sub	w0, w1, w0
	str	w0, [sp, 28]
	ldr	w0, [sp, 28]
	add	sp, sp, 32
	ret
	.size	func, .-func
	.section	.rodata
	.align	3
.LC0:
	.string	"You win!"
	.align	3
.LC1:
	.string	"You Lose :("
	.text
	.align	2
	.global	main
	.type	main, %function
main:
	stp	x29, x30, [sp, -48]!
	add	x29, sp, 0
	str	w0, [x29, 28]
	str	x1, [x29, 16]
	ldr	x0, [x29, 16]
	add	x0, x0, 8
	ldr	x0, [x0]
	bl	atoi
	str	w0, [x29, 44]
	ldr	w0, [x29, 44]
	bl	func
	cmp	w0, 0
	bne	.L4
	adrp	x0, .LC0
	add	x0, x0, :lo12:.LC0
	bl	puts
	b	.L6
.L4:
	adrp	x0, .LC1
	add	x0, x0, :lo12:.LC1
	bl	puts
.L6:
	nop
	ldp	x29, x30, [sp], 48
	ret
	.size	main, .-main
	.ident	"GCC: (Ubuntu/Linaro 7.5.0-3ubuntu1~18.04) 7.5.0"
	.section	.note.GNU-stack,"",@progbits
```

On checking the program bit by bit, 
for the code,  
```
str w0, [sp, 12]
mov w0, 81
str w0, [sp, 16]
str wzr, [sp, 20]
mov w0, 3
str w0, [sp, 24]
ldr w0, [sp, 20]
ldr w1, [sp, 16]
```  
The user input is stored at `[sp, 12]`.
and the fixed values are intialized as 
`81` is stored at `[sp, 16]`.  
`0` is stored at `[sp, 20]`. (`wzr` stands for "**zero register**". It is a special-purpose register that always holds the value 0)  
`3` is stored at `[sp, 24]`.   
The `mov` command means the value 81 is moved into w0.  
and `[sp, 16]` means `stack + 16`.  

>`ldr` stands for **Load Register**.
>It is used to load data from memory into a register. its used for transferring data between registers and memory.

`ldr	w0, [sp, 20]` Here we are loading 0 (stored at [sp, 20]) to w0 and similarly,  
`ldr	w1, [sp, 16]` 81 to w1.  

Coming to next part of the code,  
```  
lsl	w0, w1, w0
	str	w0, [sp, 28]
	ldr	w1, [sp, 28]
	ldr	w0, [sp, 24]
```
As the hint indicated, we are going to deal with shift operators.  
>Here, `lsl` stands for **Logical Shift Left**. It is used to shift the bits of a register/value to the **left** by a specified no. of positions. 
>All this is equivalent to multiplying the value by **2 to the power n**, where n is the number of positions shifted.  

Syntax: `lsl x,y,z`
which means shift the value in y by z and store the result in x.  
w1 = `[sp, 16]` (81).
w0 = `[sp, 20]` (0).   
So,` lsl w0, w1, w0` means w0 = 81 << 0 = 81.  
store the result at `[sp, 28]`.  

ldr	w1, [sp, 28] loading 81 into w1,    
ldr	w0, [sp, 24] loading 3 into w0.  

Moving to next  
```
sdiv	w0, w1, w0
str	w0, [sp, 28]
ldr	w1, [sp, 28]
ldr	w0, [sp, 12]
```  

>`sdiv` means **signed division**.
Syntax: `sdiv x,y,z`  
Divide y by z and store in x.  

In this case, w1//w0, i.e., 81//3 = 27 stored in w0.[sp, 28]  

Next, loading the value in [sp, 28] to w1, w1=27 and similarly w0=user input.  

The last part of understanding,  
```
sub	w0, w1, w0
str	w0, [sp, 28]
ldr	w0, [sp, 28]
add	sp, sp, 32
ret
```

>`sub` means subtraction.  
Syntax: `sub x, y, z`
y-z and store in x.

Hence w0= 27 - user input, storing the result in stack + 28 and load that result back into w0.  
Return.   

Now, since the result of the subtraction is returned to the `main` function, the program prints `win` if the result is 0.  
Hence, 27−input=0
which implies that **input=27** .

According to the given flag format, 
converting 27 to hexadecimal, we get **1b**.  
Placing 0s in the starting, we get the following flag:  
**`picoCTF{0000001b}`**











