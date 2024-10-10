  # Linux Luminarium  
  ## Practicing_Piping  

**stdout**: Standard Output  
**stdin** : Standard Input  
**stderr**: Standard Error
  ### 1. Redirecting Output  
  To redirect output, we use `>` character.  This basically transfers the output of the left hand side 
  command to the right hand side command. When we print the right hand side command, output of left is displayed.  
  Here we need to redirect the output from **PWN** to **COLLEGE** file
  ```
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your 
flag:
pwn.college{8osFbvwnh4urXx0YYNyTf0hevfF.dRjN1QDLyIzN0czW}
```

### 2. Redirecting more output  
In this we need to redirect the standard output of `/challenge/run`(that prints the flag) to **myflag** file. Then we use `cat` command to get the flag from myflag.
```
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.

hacker@piping~redirecting-more-output:~$ ls
COLLEGE  Desktop  a  myflag
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{01KLBAuBvXCzP2gwdON5yj6Jeb6.dVjN1QDLyIzN0czW}
```

### 3. Appending output  
When we want to add more than one file's output to another file, we can use `>>` character. This adds the other file's output instead of replacing the previous files.  
Here, in order to get the flag, we need to redirect **/challenge/run** to **/home/hacker/the-flag** two times, the other time appending in order to get the second half.  

```
hacker@piping~appending-output:~$ /challenge/run > /home/hacker/the-flag
hacker@piping~appending-output:~$ /challenge/run >> /home/hacker/the-flag
hacker@piping~appending-output:~$ cat /home/hacker/the-flag
 | 
\|/ This is the first half:
 v 
pwn.college{YGM4pv8waK-4yP_QAhf3y1LKupU.ddDM5QDLyIzN0czW}
                              ^
     that is the second half /|\
                              |
```

### 4. Redirecting errors  
File Descriptor methods are used to describe a communciation channel. Some of them are:  
**FD 0**: Standard Input
**FD 1**: Standard Output
**FD 2**: Standard Error  
`>` without a number implies 1>, which redirects **FD 1** (Standard Output).
`2>` means redirecting standard errors.  

```
hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2> instructions
hacker@piping~redirecting-errors:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{YEtJ8mKERTJ2rF1qRUybo_Gn6Sq.ddjN1QDLyIzN0czW}
```

### 5. Redirecting input  
We can redirecting input by using `<` character.  
We need to redirect the COLLEGE file to PWN file and PWN to /challenge/run.  

```
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read 
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{8zCkGkDw0Ohr5ySY0IyNq-t2_p2.dBzN1QDLyIzN0czW}
```

### 6. Grepping stored results  
`grep` command is used to find a file in a directory. Here we make use of both `>` and `grep` command to get the flag. First redirecting to /tmp/data.txt file and then searching for the flag by using pwn.college keyword.  

```
 hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /tmp/data.txt
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to a file called /tmp/data.txt. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~grepping-stored-results:~$ grep pwn.college /tmp/data.txt
pwn.college{MBCTqAWAxwvjPzyqgY3uD2n1Cuj.dhTM4QDLyIzN0czW}
```

### 7. Grepping live output  
The pipe `|` operator is used to tranfer the output of a file(left hand side) to another file(right hand side).   
In this, /challenge/run which has the output (flag) is taken as the input for grep command, which hence prints the flag.   
```
hacker@piping~grepping-live-output:~$ /challenge/run | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{I7d3VytLaOmq1ARNP-wpLJuj_Fy.dlTM4QDLyIzN0czW}
```

### 8. Grepping errors  
Since the `|` operator can only transfer the standard output of a command, we cannot use it to tranfer standard errors. So here we make use of &> operator
```
hacker@piping~grepping-errors:~$ /challenge/run 2>& 1 | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{UNmdNG4vyrZ7yMM-LVcNfSHNDQV.dVDM5QDLyIzN0czW}