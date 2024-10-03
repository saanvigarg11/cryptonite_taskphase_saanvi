# Linux Luminarium
## Module 2: Pondering Paths

Linux filesystem has a **root directory** and can contains several other directories and files within it.  
We can refer to files and directories by their path which starts with /. 

### The Root  
We have to trigger a program by providing its path. In this case, we have to invoke /pwn, which is the given path in the question.  
When the path starts with `/`, it is an absolute path. Hence `/pwn` is an **absolute path** and it is in the root directory.  

```
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{IV_FFSaGjhvhMDFWNLrooA97_9L.dhzN5QDLyIzN0czW}
```
### Program and Absolute paths  
Now, we are given a challenge directory which is located inside the root directory, i.e. `/`.  
Hence the path now become `/challenge`. Further, there is a program named **run**.  
We need to execute this run program file.

```
hacker@paths~program-and-absolute-paths:~$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{UXslIlVyjcclE8uOaFK8faNzoiW.dVDN1QDLyIzN0czW}
```

### Postion thy self  
`cd` command: It stands for **c**hange **d**irectory.  
Since Linux filesystem has many sub-directories located within it, we sometimes have to go through different directories by providing its path as its argument.  
When we execute cd command, the **~$** changes to **new_directory_path$**
Now this shows the current directory we are working in.

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
