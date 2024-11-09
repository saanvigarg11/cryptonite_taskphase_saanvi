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

### 3. Cracking Passwords  
We can get the password for the file by using the **John the Ripper** method. The leaked passwords are stored in /etc/shadow file, here in /challenge/shadow-leak. So we just need to specify the file name after john.  
Here, we need to get the password for zardus file and then run the command /challenge/run to get the flag.
```
hacker@users~cracking-passwords:~$ john /challenge/shadow-leak
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
0g 0:00:00:02 28% 1/3 0g/s 276.9p/s 276.9c/s 276.9C/s sudraz!..bzardus
0g 0:00:00:13 0% 2/3 0g/s 276.5p/s 276.5c/s 276.5C/s sniper..bigben
0g 0:00:00:14 0% 2/3 0g/s 277.3p/s 277.3c/s 277.3C/s meggie..seattle
0g 0:00:00:19 1% 2/3 0g/s 279.5p/s 279.5c/s 279.5C/s rosita..help
aardvark         (zardus)
1g 0:00:00:20 100% 2/3 0.04803g/s 279.6p/s 279.6c/s 279.6C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker@users~cracking-passwords:~$ su zardus
Password: 
zardus@users~cracking-passwords:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{wj2Pw232SZahywm3Qje99mcQoSl.ddTN0UDLyIzN0czW}
```

### 4. Using Sudo  
Now, instead of using su to first change the user and then get the flag, we can directly run a command as the root user by using the **`sudo`**(**s**uperuser **d**o) command.
We just need to write sudo before the command.    
```
hacker@users~using-sudo:~$ sudo cat /flag
pwn.college{Yk2aZweDi9klBnseOsTc6uxoGTI.dhTN0UDLyIzN0czW}
```

