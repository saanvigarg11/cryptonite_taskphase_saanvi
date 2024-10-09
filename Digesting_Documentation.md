# Linux Luminarium  
## Digesting Documentation  

### 1. Learning from Documentation  
This basically tells that we need to specify proper arguments in order to use a program.  
For eg: here we need to run `/challenge/challenge` program and specify the argument `--giveflag` in order to properly 
run the program.  
```
hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{4z1RMKaioyq5mUeplpygZBZDKR0.dRjM5QDLyIzN0czW}
```

### 2. Learning Complex Usage  
We can print arbitrary files by using **--printfile** argument.  
Here we need to print the flag by using this argument correctly.  

```
hacker@man~learning-complex-usage:/$ /challenge/challenge --printfile /flag
Correct argument! Here is the /flag file:
pwn.college{QYSMy7JsEz3h47Rhv1qQB3VbDJG.dVjM5QDLyIzN0czW}
```
### 3. Reading manuals  
`man` command is used to print the manual for the command that we pass as an argument.  
In this we need to print the manual for challenge, which shows the process to print the flag.  
```
hacker@man~reading-manuals:~$ man challenge

CHALLENGE(1)                                                  Challenge Commands                                                  CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --qszsho NUM
              print the flag if NUM is 852

AUTHOR
       Written by Zardus.
hacker@man~reading-manuals:~$ /challenge/challenge --qszsho 852
Correct usage! Your flag: pwn.college{8qsB5zshYLGoF_tOGXh2OUUBCFL.dRTM4QDLyIzN0czW}
hacker@man~reading-manuals:~$
```


