# Linux Luminarium  
## Untangling Users  

### 1. Becoming root with su  
When **`su`**(**s**witch **u**ser) command runs as root, it can start a root shell. But it asks for 
the password from the user before allowing to access the shell. After entering the shell we can use the `cat` command to get the flag.  
```
hacker@users~becoming-root-with-su:~$ su
Password: 
root@users~becoming-root-with-su:/home/hacker# cat /flag
pwn.college{ImvTNXCkiKYTCfZmFw6PBJKgXA1.dVTN0UDLyIzN0czW}
```

### 2. Other users with su  
By default, the su command switches to the root user if no name is specified. We can also specify the username after su to switch
to that **particular user**.  
The syntax is `su [username]`.  
```
hacker@users~other-users-with-su:~$ su zardus
Password: 
zardus@users~other-users-with-su:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{4wWJQtf0EnA5pkRdRS1IFn0rE02.dZTN0UDLyIzN0czW}
```

### 3. 


