# Linux Luminarium
## Module 1: Hello Hackers

### Intro to Commands
Firstly, when we open the terminal, it starts with
`hacker@dojo:~$` which is a prompt that is prompting the user to enter a command.

**1. Whoami command**   
It is basically prints the username, which is `hacker` for the current user.

**Hello**  
Invoking this command just prints hello. Also the commands are case-sensitive.
So if we print Hello or HELLO, it will show incorrect.  

```hacker@hello~intro-to-commands:~$ whoami   
hacker  
hacker@hello~intro-to-commands:~$ hello  
Success! Here is your flag:  
pwn.college{kUrc3rFi9pv1hKExbQH7vz8Xz1-.ddjNyUDLyIzN0czW}
```

### Intro to Arguments
Now, instead of simply printing hello, we use commands to print arguments, which are additional data passed to the command.  
For eg: `echo hello` , in which echo is the command and hello is the argument.

Similarly, in this if we execute hello with hackers, then `hello` becomes the command and `hackers` becomes the argument. 
This prints hackers.

```
hacker@hello~intro-to-arguments:~$ hello hackers
Success! Here is your flag:
pwn.college{AUMUZY4O_yJH6olvue2LrcIyTLY.dhjNyUDLyIzN0czW}
```
