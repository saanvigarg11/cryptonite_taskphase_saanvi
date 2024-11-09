# Linux Luminarium
## Module 2: Pondering Paths

Linux filesystem has a **root directory** and can contains several other directories and files within it.  
We can refer to files and directories by their path which starts with /. 

### 1. The Root  
We have to trigger a program by providing its path. In this case, we have to invoke /pwn, which is the given path in the question.  
When the path starts with `/`, it is an absolute path. Hence `/pwn` is an **absolute path** and it is in the root directory.  

```
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{IV_FFSaGjhvhMDFWNLrooA97_9L.dhzN5QDLyIzN0czW}
```
### 2. Program and Absolute paths  
Now, we are given a challenge directory which is located inside the root directory, i.e. `/`.  
Hence the path now become `/challenge`. Further, there is a program named **run**.  
We need to execute this run program file.

```
hacker@paths~program-and-absolute-paths:~$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{UXslIlVyjcclE8uOaFK8faNzoiW.dVDN1QDLyIzN0czW}
```

### 3. Postion thy self  
`cd` command: It stands for **c**hange **d**irectory.  
Since Linux filesystem has many sub-directories located within it, we sometimes have to go through different directories by providing its path as its argument.  
When we execute cd command, the **~$** changes to **new_directory_path$**, this shows the current directory we are working in.

>`pwd` stands for **p**rint **w**orking **d**irectory that shows the current directory in which we are working.

Here we are asked to run the program in another directory, which is not known to us.  
For that we first run 
```
hacker@paths~position-thy-self:~$ /challenge/run
Incorrect...
You are not currently in the /usr/aarch64-linux-gnu/include/gnu directory.
Please use the `cd` utility to change directory appropriately.
```

Using this we come to know to which directory we have to change.
Now we use the **cd** command with the new directory and then run the program.  

```
hacker@paths~position-thy-self:~$ cd /usr/aarch64-linux-gnu/include/gnu
hacker@paths~position-thy-self:/usr/aarch64-linux-gnu/include/gnu$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{8wkSft4d6rn6uYapYkO9KaFG68x.dZDN1QDLyIzN0czW}
```

_The next two programs have the concept as above._  

### 4. Position elsewhere  
The procedure and logic is same.
```
hacker@paths~position-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /usr/share/doc directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-elsewhere:~$ cd /usr/share/doc
hacker@paths~position-elsewhere:/usr/share/doc$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{8vGncmDNDa28Df80p0GU_ebk49g.ddDN1QDLyIzN0czW}
```

### 5. Position yet elsewhere
The procedure and logic is same.
```
hacker@paths~position-yet-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /var/log directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-yet-elsewhere:~$ cd /var/log
hacker@paths~position-yet-elsewhere:/var/log$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{EpaYKMlGkc5cBGetGVWoUVyJcr8.dhDN1QDLyIzN0czW}
```

### 6. implicit relative paths, from /  
Till now we were working with absolute paths that were starting with /. Now, we need to run the program which is in a **relative path**.  
A relative path is interpreted relative to our **c**urrent **w**orking **d**irectory (**cwd**). The only difference is that absolute paths start with /, but relative paths never start with /. It depends on the path of cwd.  

First, I tried directly executing the program, but then i didn't specify the directory. Then I executed the program starting wiht /, so it prompted that our cwd is already `/`.
```
hacker@paths~implicit-relative-paths-from-:~$ challenge/run
bash: challenge/run: No such file or directory
hacker@paths~implicit-relative-paths-from-:~$ /challenge/run
Incorrect...
You are not currently in the / directory.
Please use the `cd` utility to change directory appropriately.
```
So now I first changed the directory name to `/`, and then printed `challenge/run` without using / n beginning.  
```
hacker@paths~implicit-relative-paths-from-:~$ cd /
hacker@paths~implicit-relative-paths-from-:/$ challenge/run
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{gxJk6l7SuEuSZ0dlqo2iDw9_4MN.dlDN1QDLyIzN0czW}
```

### 7. explicit relative paths, from /  
Here again, first I changed the directory from `/home/hacker` to `/`.  
```
hacker@paths~explicit-relative-paths-from-:~$ cd /
hacker@paths~explicit-relative-paths-from-:/$ challenge/run
Incorrect...
This challenge must be called with a relative path that explicitly starts with a `.`!
```
This prompted to start the command with a `.`.
So then I ran
```
hacker@paths~explicit-relative-paths-from-:/$ ./challenge/run
Correct!!!
./challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{Ysaw92MTdIjw1S5DnhWjVrpfOfb.dBTN1QDLyIzN0czW}
```

### 8. implicit relative path  
It prompts us to use `.` command instead of simply writing `run`. If we only write `run`, it will show the following error:  
```
hacker@paths~implicit-relative-path:~$ /challenge/run
Incorrect...
You are not currently in the /challenge directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~implicit-relative-path:~$ cd /challenge
hacker@paths~implicit-relative-path:/challenge$ run
bash: run: command not found
```

This is basically done for safety. If this was not done, we could sometimes execute programs in our cd that have the same names as core system utilities. Hence we need to provide an explicit path `./` .  
```
hacker@paths~implicit-relative-path:/challenge$ ./run
Correct!!!
./run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{Uptu7o0rK2V54S2xlqsiTl3cwim.dFTN1QDLyIzN0czW}
```

### 9. home sweet home  
`~` is a shorthand for `/home/hacker`, which is the current working directory. The expansion of ~ is an **absolute path**. For example: `~/~` will be expanded to `/home/hacker/~` .  
Now, need to give the absolute path as an argument when executing `/challenge/run` and the file path should point to the home directory which should not be more than 3 characters. Let the name of the file be a. So the absolute path would be `/a`.  
```
hacker@paths~home-sweet-home:~$ pwd
/home/hacker
hacker@paths~home-sweet-home:~$ cd /tmp
hacker@paths~home-sweet-home:/tmp$ /challenge/run ~/ab
The argument you provided must not have been longer than 3 characters (it's 
currently 4 characters long)!
hacker@paths~home-sweet-home:/tmp$ /challenge/run ~/a
Writing the file to /home/hacker/a!
... and reading it back to you:
pwn.college{0M0Ma3lRyM3z-B4H-BPmlMg_8K3.dNzM4QDLyIzN0czW}
```

