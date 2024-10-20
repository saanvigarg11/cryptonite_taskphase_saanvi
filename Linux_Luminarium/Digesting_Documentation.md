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
Hence to print the flag I used the steps given in description and entered 852 in place of NUM.  

### 4. Searching Manuals  
We can search for the flag by using the /flag command in the manual. This way we got the line which gave the right argument.  
```
hacker@man~searching-manuals:~$ man challenge

/flag  _(for finding the word flag)_
--lapjpkc
              This argument will give you the flag!


hacker@man~searching-manuals:~$ /challenge/challenge --lapjpkc
Initializing...
Correct usage! Your flag: pwn.college{gRtBJMSX7i1ZHRbz-40yfPKN3qW.dVTM4QDLyIzN0czW}
```

### 5. Searching for Manuals  
Till now we were searching for directions inside the manual, now we need to find manuals inside manuals for further hints. For this we can use the command `man -k`, as given in the synopsis, to find the word challenge in the manual.
```
hacker@man~searching-for-manuals:~$ man man
.
.
.
hacker@man~searching-for-manuals:~$ man -k
apropos what?
hacker@man~searching-for-manuals:~$ man -k challenge
kiygkzhrxo (1)       - print the flag!
hacker@man~searching-for-manuals:~$ man kiygkzhrxo

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

       --kiygkz NUM
              print the flag if NUM is 372

hacker@man~searching-for-manuals:~$ /challenge/challenge --kiygkz 372
Correct usage! Your flag: pwn.college{A-kiygkzOhCrxo-37TgY2QWIRRz.dZTM4QDLyIzN0czW}
```

### 6. Helpful programs  
`--help` or `-h` is used mostly when progams don't have a manual page. So we run `/challenge/challenge --help` to infer how to get the flag.  
Then using -p to print the value that will cause the -g option to print the flag.  

```
hacker@man~helpful-programs:~$ /challenge/challenge --help
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]

optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to give you the flag
hacker@man~helpful-programs:~$ /challenge/challenge -v
I'm exactly the version I need to be!

hacker@man~helpful-programs:~$ /challenge/challenge -p
The secret value is: 660
hacker@man~helpful-programs:~$ /challenge/challenge --give-the-flag 660
Correct usage! Your flag: pwn.college{cG6Gp6cDyeL_0swCw24w7y1uA8g.ddjM4QDLyIzN0czW}
```

### 7. Help for Bulletins  
Commands that don't have man pages and help options, are built into the shell itself, hence are called builtins. We can get a list of shell builtins by running the builtin help.   
Here we use `help challenge` to display the directions for getting the flag.  

```
hacker@man~help-for-builtins:~$ help challenge
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!
    
    Options:
      --fortune         display a fortune
      --version         display the version
      --secret VALUE    prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "MY_n_oYE".
hacker@man~help-for-builtins:~$ /challenge/challenge --secret MY_n_oYE
bash: /challenge/challenge: No such file or directory
hacker@man~help-for-builtins:~$ challenge --secret MY_n_oYE
Correct! Here is your flag!
pwn.college{MY_n_oYECNgTAn_PAFVSeq7yeK0.dRTM5QDLyIzN0czW}
```


