  # Linux Luminarium  
  ## Practicing_Piping  

**stdout: Standard Output  
stdin: Standard Input  
stderr: Standard Error**
  ### 1. Redirecting Output  
  To redirect output, we use **>** character.  This basically transfers the output of the left hand side 
  command to the right hand side command. When we print the right hand side command, output of left is displayed.  
  Here we need to redirect the output from **PWN** to **COLLEGE** file
  ```
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your 
flag:
pwn.college{8osFbvwnh4urXx0YYNyTf0hevfF.dRjN1QDLyIzN0czW}
```

### 2. Redirecting more output  

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

  
  
