# Linux Luminarium  
## Chaining Commands  

### 1. Chaining with Semicolons   
We can execute more than 1 command together by using **semicolons(;)** in between. The major difference is that when we hit Enter, the 
first command executes and then it prompts for the second, whereas while using ; both are executed without a prompt.  
```
hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn; /challenge/college
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{QXa4_y-3NpNoMkOp1KS93O1VsxY.dVTN4QDLyIzN0czW}
```

### 2. Your First Shell Script  
We can create a shell script(here x) by using nano text editor and store the files in it. Then we can execute them by using 
**bash** command.   
```
hacker@chaining~your-first-shell-script:~$ touch x.sh
hacker@chaining~your-first-shell-script:~$ nano x.sh
hacker@chaining~your-first-shell-script:~$ bash x.sh
Great job, you've written your first shell script! Here is the flag:
pwn.college{I_H1Ec1tjhfa7oJ1LfKgofJU-uq.dFzN4QDLyIzN0czW}
```

### 3. Redirecting Script Output  
Now, we can collectively use the both the commands to generate the output and then pipe or redirect it into another path. For this
 we first need to create the files in text editor and then call it using the bash command to pipe the output.  
 ```
hacker@chaining~redirecting-script-output:~$ cat x.sh
/challenge/pwn
/challenge/college

hacker@chaining~redirecting-script-output:~$ bash x.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{4_DARE8XedC0NHlHfKXFSzLPj24.dhTM5QDLyIzN0czW}
```

### 4. 


