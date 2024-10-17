# Linux Luminarium  
## Pondering PATHS  

### 1. The PATH Variable  
A special shell variable, called **PATH**, that stores many directory paths in which the shell searches for programs 
corresponding to commands. In this challenge, on running the /challenge/run, it will run the rm command that will delete the flag
stored in it. So to prevent this, we blank out the PATH variable.  
```
hacker@path~the-path-variable:~$ PATH=""
hacker@path~the-path-variable:~$ ls
bash: ls: No such file or directory
hacker@path~the-path-variable:~$ rm
bash: rm: No such file or directory
hacker@path~the-path-variable:~$ /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{IFW_s4m_oawhsr-q4QS2Bc35Flj.dZzNwUDLyIzN0czW}
```

### 2. Setting PATH  
We can store the file's path in a variable and then execute them via their path.  
```
hacker@path~setting-path:~$ PATH=/challenge/more_commands/
hacker@path~setting-path:~$ /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{4j5QMzChpy5FVop3UWX-hgQh8U8.dVzNyUDLyIzN0czW}
```

### 3. Adding Commands  
First we again need to create a nano file named win and add the following code in it.  
```read -r flag < /flag
echo "$flag"
```
We can just read the flag and the echo it, since we can't directly use the cat command.  
Now we need to make them executable by using `+x` argument with `chmod` command.  
Finally, we state the PATH variable and then /challenge/run to get the flag.  
```
hacker@path~adding-commands:~$ nano win
hacker@path~adding-commands:~$ chmod +x win
hacker@path~adding-commands:~$ PATH=/home/hacker
hacker@path~adding-commands:~$ /challenge/run
Invoking 'win'....
pwn.college{o97iOmaISIKKL6RXJiwwXVkj8vj.dZzNyUDLyIzN0czW}
```

### 4. Hijacking Commands  
Here, we just need to repeat the previous procedure by only changing the command from `win` to `rm`.  
That is, `nano rm` in order to trick the command.  
```
hacker@path~hijacking-commands:~$ nano rm
hacker@path~hijacking-commands:~$ chmod +x rm
hacker@path~hijacking-commands:~$ PATH=/home/hacker
hacker@path~hijacking-commands:~$ /challenge/run
Trying to remove /flag...
pwn.college{4ZzOMwoYSUTh3Hv0AlhrZ8II2Ic.ddzNyUDLyIzN0czW}
```
