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

