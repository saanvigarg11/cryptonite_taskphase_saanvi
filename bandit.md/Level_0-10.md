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
In this, the password can be in any of the files from file00 to file09. So I used cat command for all the files one by one to find the password:   
```
bandit4@bandit:~/inhere$ cat ./-file07
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw  
```
_Alternatively, we can also use the following `find` and `grep` commands to find the file with ASCII charcaters as all the other files have non-printable characters._  
```
bandit4@bandit:~/inhere$ find . -type f -exec file {} + | grep ASCII
./-file07: ASCII text
```

## Level 5-6  
Here, I first changed the directory into inhere, then used `find` command to get the right file.  
```
bandit5@bandit:~$ cd inhere
bandit5@bandit:~/inhere$ ls -la
total 88
drwxr-x--- 22 root bandit5 4096 Sep 19 07:08 .
drwxr-xr-x  3 root root    4096 Sep 19 07:08 ..
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere00
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere01
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere02
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere03
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere04
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere05
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere06
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere07
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere08
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere09
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere10
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere11
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere12
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere13
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere14
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere15
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere16
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere17
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere18
drwxr-x---  2 root bandit5 4096 Sep 19 07:08 maybehere19
bandit5@bandit:~/inhere$ find -readable -size 1033c
./maybehere07/.file2
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

## Level 6-7  
Here, we don't know the exact directory where the file with the password is located. So we first command   
`find / -type f -user bandit7 -group bandit6 -size 33c`, but it showed many files with permission denied. Hence to find the file which we have access to, I used the following:  
```
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

## Level 7-8  
When we try to cat data.txt, it lists a lot of files. So instead of that, I used the `piping` operator with `cat` and `grep` command.  
```
bandit7@bandit:~$ ls -a
.  ..  .bash_logout  .bashrc  data.txt  .profile
bandit7@bandit:~$ cat data.txt | grep millionth
millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc  
```

## Level 8-9  
In this challenge, we had to use the `sort` and `uniq` command.  
The **sort** command sorts the contents of the file data.txt, making the **duplicate lines adjacent** to each other.  
The **uniq** command filters out those lines which are repeated. The -u flag displays the lines that appear only once.  
```
bandit8@bandit:~$ ls -a
.  ..  .bash_logout  .bashrc  data.txt  .profile
bandit8@bandit:~$ sort data.txt | uniq -u
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

## Level 9-10  
I made the use of **`strings`** command which allows us to print all the readable ASCII characters from the file, and then the `grep` command as the password is preceded by **=** signs.  
```
bandit9@bandit:~$ strings data.txt | grep =
}========== the
p\l=
;c<Q=.dEXU!
3JprD========== passwordi
qC(=
~fDV3========== is
7=oc
zP=
~de=
3k=fQ
~o=0
69}=
%"=Y
=tZ~07
D9========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
N=~[!N
zA=?0j
```




