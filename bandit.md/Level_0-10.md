# Bandit Game  
We have to login to the game by using SSH. Then we need to connect to the host **bandit.labs.overthewire.org** on port **2220**.  
For which I used the command **`ssh bandit0@bandit.labs.overthewire.org -p 2220`**.  
General command for logging in is: `ssh bandit[level number]@bandit.labs.overthewire.org -p 2220`.

## Level 0-1  
To get password from the directory named readme, I used `cat` command.  
```
bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

## Level 1-2  
I logged in again and used the command:  
```
ssh bandit1@bandit.labs.overthewire.org -p 2220
```
Then to get the next password:  
```
bandit1@bandit:~$ cat ./-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

## Level 2-3  
For a filename with spaces, we can use double quotes.  
```
bandit2@bandit:~$ cat "spaces in this filename"
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

## Level 3-4  
Here, the password is in a file of a directory inhere. So we first need to change to that directory using `cd` command.  
Then for hidden files to show, we use `-a` with ls.  
```
bandit3@bandit:~$ ls -la
total 24
drwxr-xr-x  3 root root 4096 Sep 19 07:08 .
drwxr-xr-x 70 root root 4096 Sep 19 07:09 ..
-rw-r--r--  1 root root  220 Mar 31  2024 .bash_logout
-rw-r--r--  1 root root 3771 Mar 31  2024 .bashrc
drwxr-xr-x  2 root root 4096 Sep 19 07:08 inhere
-rw-r--r--  1 root root  807 Mar 31  2024 .profile
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$ ls
bandit3@bandit:~/inhere$ ls -a
.  ..  ...Hiding-From-You
bandit3@bandit:~/inhere$ cat ...Hiding-From-You
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

## Level 4-5  


## Level 5-6  
In this, the password can be in any of the files from file00 to file09. So I used cat command for all the files one by one to find the password:   
```
bandit4@bandit:~/inhere$ cat ./-file07
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw  
```
_Alternatively, we can also use the following find and grep commands to find the file with ASCII charcaters as all the other files have non-printable characters._  
```
bandit4@bandit:~/inhere$ find . -type f -exec file {} + | grep ASCII
./-file07: ASCII text
```
