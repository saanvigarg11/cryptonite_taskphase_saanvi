# Reverse Engineering  

## GDB baby step 1  
<img width="433" alt="image" src="https://github.com/user-attachments/assets/9379e326-6df5-4f95-9129-1fc3e9c2aa90" />  

This challenge mainly makes the use of **GDB(GNU Debugger)** which is widely used in **debugging programs** of C, C++, etc.  
It basically can pause the program at **specific points**, which are the breakpoints,  
look at **variables** and **registers**, and   
step through the code to see how it runs.  
Went through some resources https://www.exploit-db.com/papers/13205.  

I renamed the file as **debug** and then ran gdb command in WSL to find the eax register.  
Initially, on searching for the breakpoint for main function as specified in the hint, the following output was showed:  
```
gdb debug
GNU gdb (Ubuntu 12.1-0ubuntu1~22.04.2) 12.1
Copyright (C) 2022 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from debug...
(No debugging symbols found in debug)
(gdb) run
Starting program: /mnt/c/Users/Laptop/Downloads/debug
warning: opening /proc/PID/mem file for lwp 172.172 failed: No such file or directory (2)
Failed to read a valid object file image from memory.
[Inferior 1 (process 172) exited with code 0102]
(gdb) dissamble main
Undefined command: "dissamble".  Try "help".
(gdb) break main
Breakpoint 1 at 0x8001131
(gdb) info registers eax
The program has no registers now.
(gdb) info registers
The program has no registers now.
(gdb) print 0x8001131
$1 = 134222129  
```
The program wouldn't run and also it wasn't the flag. I then checked whether I was executing the right file by using `file`
command and specifying the path of the file instead of its name on my system.  
Since it showed no registers, I decided to search for the functions that existed and locate the main function.  

Thereafter, I **dissambled the main function** to look for `eax` regsiter and the **number of contents** in decimal number base, which would give the flag.   

```
gdb debug
.
.
.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from debug...
(No debugging symbols found in debug)
(gdb) info functions
All defined functions:

Non-debugging symbols:
0x0000000000001000  _init
0x0000000000001030  __cxa_finalize@plt
0x0000000000001040  _start
0x0000000000001070  deregister_tm_clones
0x00000000000010a0  register_tm_clones
0x00000000000010e0  __do_global_dtors_aux
0x0000000000001120  frame_dummy
0x0000000000001129  main
0x0000000000001140  __libc_csu_init
0x00000000000011b0  __libc_csu_fini
0x00000000000011b8  _fini
(gdb) disas main
Dump of assembler code for function main:
   0x0000000000001129 <+0>:     endbr64
   0x000000000000112d <+4>:     push   %rbp
   0x000000000000112e <+5>:     mov    %rsp,%rbp
   0x0000000000001131 <+8>:     mov    %edi,-0x4(%rbp)
   0x0000000000001134 <+11>:    mov    %rsi,-0x10(%rbp)
   0x0000000000001138 <+15>:    mov    $0x86342,%eax
   0x000000000000113d <+20>:    pop    %rbp
   0x000000000000113e <+21>:    ret
End of assembler dump.
(gdb) print 0x86342
$1 = 549698
```
<img width="644" alt="image" src="https://github.com/user-attachments/assets/0d8fa5bb-6202-4664-b8e0-44fa7f85581e" />  

Hence the flag was:  
**`picoCTF{549698}`**  









