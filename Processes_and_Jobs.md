# Linux Luminarium  
## Processes and Jobs  

### 1. Listing Processes  
The **`ps`** command is used to list the running processes in our terminal. It stands for **process snapshot** or **process status**.  
We can see many details in the list, such as a numerical identifier (**the Process ID(PID**)), that uniquely identifies
every running process in the Linux environment.  
There are two ways to specify arguments:
**"Standard" Syntax**: `-e` to list "**every**" process and   
`-f` for a "**full format**" output, 
including arguments.   
These can be combined into a single argument **`-ef`**.

**"BSD" Syntax**:   
`a` to list processes for all users,   
`x` to list processes that aren't running in a terminal, and   
`u` for a "user-readable" output.   
These can be combined into a single argument **`aux`**.  

Here, /challenge/run has been renamed, so we need to find the new command in ps lists.  
```
hacker@processes~listing-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 13:17 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/default/bin/dojo-init /run/dojo/bin/sleep 6h
root           7       1  0 13:17 ?        00:00:00 /run/dojo/bin/sleep 6h
root          68       1  0 13:17 ?        00:00:00 /challenge/15742-run-21049
root          72      68  0 13:17 ?        00:00:00 sleep 6h
hacker        81       1  0 13:17 ?        00:00:00 /nix/store/bmmjbvb8hishfrg78ygjlynpq3ikpl39-nodejs-20.15.1/bin/node /nix/store/3v4hdb2gmpj7
hacker       104      81  1 13:17 ?        00:00:05 /nix/store/bmmjbvb8hishfrg78ygjlynpq3ikpl39-nodejs-20.15.1/bin/node /nix/store/3v4hdb2gmpj7
hacker       145     104  2 13:17 ?        00:00:07 /nix/store/bmmjbvb8hishfrg78ygjlynpq3ikpl39-nodejs-20.15.1/bin/node --dns-result-order=ipv4
hacker       163     104  0 13:17 ?        00:00:00 /nix/store/bmmjbvb8hishfrg78ygjlynpq3ikpl39-nodejs-20.15.1/bin/node /nix/store/3v4hdb2gmpj7
hacker       223     163  0 13:17 pts/1    00:00:00 /run/dojo/bin/bash --init-file /nix/store/3v4hdb2gmpj7jv2z848ikakhzl9rjgwh-code-server/libe
hacker      1142     223  0 13:22 pts/1    00:00:00 ps -ef
hacker@processes~listing-processes:~$ /challenge/15742-run-21049
Yahaha, you found me! Here is your flag:
pwn.college{orV3oYqUYLtGNodWIJoYiYEynC0.dhzM4QDLyIzN0czW}
Now I will sleep for a while (so that you could find me with 'ps').
```

### 2. Killing Processes  
`kill` command terminates a process. We just need to find the PID of that program which is preventing 
any command to run. For that we use `ps -ef | grep /challenge/dont_run`. It specifies the PID which we then
use to kill the program.  
```
hacker@processes~killing-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 17:47 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/default/bin/dojo-init /run/dojo/bin/sleep 6h
root           7       1  0 17:47 ?        00:00:00 /run/dojo/bin/sleep 6h
root          71       1  0 17:47 ?        00:00:00 su -c /challenge/.launcher hacker
hacker        73      71  0 17:47 ?        00:00:00 /challenge/dont_run
hacker        74      73  0 17:47 ?        00:00:00 sleep 6h
hacker        83       1  1 17:47 ?        00:00:00 /nix/store/bmmjbvb8hishfrg78ygjlynpq3ikpl39-nodejs-20.15.1/bin/node /nix/store/3v4hdb2gmpj7jv2
hacker       104      83  7 17:47 ?        00:00:05 /nix/store/bmmjbvb8hishfrg78ygjlynpq3ikpl39-nodejs-20.15.1/bin/node /nix/store/3v4hdb2gmpj7jv2
hacker       145     104  4 17:47 ?        00:00:03 /nix/store/bmmjbvb8hishfrg78ygjlynpq3ikpl39-nodejs-20.15.1/bin/node --dns-result-order=ipv4fir
hacker       169     104  0 17:47 ?        00:00:00 /nix/store/bmmjbvb8hishfrg78ygjlynpq3ikpl39-nodejs-20.15.1/bin/node /nix/store/3v4hdb2gmpj7jv2
hacker       223     169  0 17:47 pts/1    00:00:00 /run/dojo/bin/bash --init-file /nix/store/3v4hdb2gmpj7jv2z848ikakhzl9rjgwh-code-server/libexec
hacker       458     223  0 17:48 pts/1    00:00:00 ps -ef
hacker@processes~killing-processes:~$ ps -ef | grep /challenge/dont_run
hacker        73      71  0 17:47 ?        00:00:00 /challenge/dont_run
hacker       634     223  0 17:49 pts/1    00:00:00 grep --color=auto /challenge/dont_run
hacker@processes~killing-processes:~$ kill 73
hacker@processes~killing-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 17:47 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/default/bin/dojo-init /run/dojo/bin/sleep 6h
root           7       1  0 17:47 ?        00:00:00 /run/dojo/bin/sleep 6h
hacker        74       1  0 17:47 ?        00:00:00 sleep 6h
hacker        83       1  0 17:47 ?        00:00:00 /nix/store/bmmjbvb8hishfrg78ygjlynpq3ikpl39-nodejs-20.15.1/bin/node /nix/store/3v4hdb2gmpj7jv2
hacker       104      83  2 17:47 ?        00:00:06 /nix/store/bmmjbvb8hishfrg78ygjlynpq3ikpl39-nodejs-20.15.1/bin/node /nix/store/3v4hdb2gmpj7jv2
hacker       145     104  2 17:47 ?        00:00:06 /nix/store/bmmjbvb8hishfrg78ygjlynpq3ikpl39-nodejs-20.15.1/bin/node --dns-result-order=ipv4fir
hacker       169     104  0 17:47 ?        00:00:00 /nix/store/bmmjbvb8hishfrg78ygjlynpq3ikpl39-nodejs-20.15.1/bin/node /nix/store/3v4hdb2gmpj7jv2
hacker       223     169  0 17:47 pts/1    00:00:00 /run/dojo/bin/bash --init-file /nix/store/3v4hdb2gmpj7jv2z848ikakhzl9rjgwh-code-server/libexec
hacker      1081     169  0 17:51 ?        00:00:00 /bin/sh -c "/nix/store/3v4hdb2gmpj7jv2z848ikakhzl9rjgwh-code-server/libexec/code-server/lib/vs
hacker      1082    1081  0 17:51 ?        00:00:00 /nix/store/1xhds5s320nfp2022yjah1h7dpv8qqns-bash-5.2p32/bin/bash /nix/store/3v4hdb2gmpj7jv2z84
hacker      1085    1082  0 17:51 ?        00:00:00 sleep 1
hacker      1087     223  0 17:51 pts/1    00:00:00 ps -ef
hacker@processes~killing-processes:~$ /challenge/run
Great job! Here is your payment:
pwn.college{wdycb8FAZWM2Nf5ztYfFAVAt2RN.dJDN4QDLyIzN0czW}
```

### 3. Interrupting Processes  
The `Ctrl+C` hotkey is used to exit the application that is expecting an input from the terminal and
hence helps in executing our program.  
```
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember, 
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{kH6zRhmP28MdzNAkS-18YTvG3qo.dNDN4QDLyIzN0czW}
```

### 4. Suspending Processes  
The `Ctrl+Z`hotkey is used to suspend a program. If another copy of the program is running, then it will 
give the flag.  
```
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in 
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root         400     213  0 17:57 pts/1    00:00:00 bash /challenge/run
root         402     400  0 17:57 pts/1    00:00:00 ps -f

I don't see a second me!

To pass this level, you need to suspend me and launch me again! You can 
background me with Ctrl-Z or, if you're not ready to do that for whatever 
reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in 
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root         400     213  0 17:57 pts/1    00:00:00 bash /challenge/run
root         535     213  0 17:57 pts/1    00:00:00 bash /challenge/run
root         537     535  0 17:57 pts/1    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:
pwn.college{oKr8g5kMviHEvvaofLITQYI3r9F.dVDN4QDLyIzN0czW}
```

### 5. Resuming Processes  
To resume a suspended processes in the _foreground_, we use `fg` command.  
```
hacker@processes~resuming-processes:~$ /challenge/run
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with 
the 'fg' command! Or just press Enter to quit me!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~resuming-processes:~$ fg
/challenge/run
I'm back! Here's your flag:
pwn.college{QKxk5Q2FZGkL6-mnrGuGSLHY0t8.dZDN4QDLyIzN0czW}
Don't forget to press Enter to quit me!

Goodbye!
```

### 6. Backgrounding Processes  
We use the `bg` command to resume processes that were suspended in the _background_.  
```
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and 
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         819 S+   bash /challenge/run
root         821 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the 
background, and then launch a new version of me! You can background me with 
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to 
do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~backgrounding-processes:~$ bg
[1]+ /challenge/run &



Yay, I'm now running the background! Because of that, this text will probably 
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times 
to scroll this text out.
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and 
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         819 S    bash /challenge/run
root         919 S    sleep 6h
root         951 S+   bash /challenge/run
root         953 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background! Here is the flag:
pwn.college{EUSYEy97gStJ7BPm8PIKxuRyGoe.ddDN4QDLyIzN0czW}
```

### 7. Foregrounding Processes  
Here, we need to first suspend the process by `Ctrl+Z`, then resume in background `bg` and then again resume
resume it in `fg`.  
```
hacker@processes~foregrounding-processes:~$ /challenge/run
To pass this level, you need to suspend me, resume the suspended process in the 
background, and *then* foreground it without re-suspending it! You can 
background me with Ctrl-Z (and resume me in the background with 'bg') or, if 
you're not ready to do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~foregrounding-processes:~$ bg
[1]+ /challenge/run &



Yay, I'm now running the background! Because of that, this text will probably 
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times 
to scroll this text out. After that, resume me into the foreground with 'fg'; 
I'll wait.
hacker@processes~foregrounding-processes:~$ fg
/challenge/run
YES! Great job! I'm now running in the foreground. Hit Enter for your flag!

pwn.college{Ak1PYXK-aF1vi7eUFckkKrz0Xfg.dhDN4QDLyIzN0czW}
```

### 8. Starting Background Processes  
We can start the backgrounded process by appending a **`&`** to the command.  
```
hacker@processes~starting-backgrounded-processes:~$ /challenge/run &
[1] 316



hacker@processes~starting-backgrounded-processes:~$ Yay, you started me in the background! Because of that, this text will probably 
overlap weirdly with the shell prompt, but you're used to that by now...

Anyways! Here is your flag!
pwn.college{cuGvjXmxi18n49bv36peW7dyXyP.dlDN4QDLyIzN0czW}

[1]+  Done                    /challenge/run
```

### 10. Process Exit Codes  
The **`?`** variable, prepended with a `$`, is used to access the exit code of the 
most recently-terminated command. In this challenge, we need to first retrieve the exit code of 
`/challenge/get-code` and then enter the code after `/challenge/submit-code` command to get the flag.  
```
hacker@processes~process-exit-codes:~$ /challenge/get-code
Exiting with an error code!
hacker@processes~process-exit-codes:~$ echo $?
48
hacker@processes~process-exit-codes:~$ /challenge/submit-code 48
CORRECT! Here is your flag:
pwn.college{QL7cqEl453PCfegB6vNEioPY5YW.dljN4UDLyIzN0czW}
```




