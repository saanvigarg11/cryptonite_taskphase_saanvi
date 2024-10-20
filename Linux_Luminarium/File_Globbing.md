# Linux Luminarium  
## File Globbing  

**Globbing lets us reference files without typing their full name, or full paths.**  

### 1. Matching with *  
When we want to print a file using `*` character, it means that any file starting with the characters before *  will be displayed. This minimizes our task to write full file's name to print them.
```
hacker@globbing~matching-with-:~$ cd /challenge
You specified the path to 'cd' to in more than 4 characters. Disallowed!
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{4LN-iVYiUxXJHSEcVBSN_JR8oxg.dFjM4QDLyIzN0czW}
```

### 2. Matching with ?  
`?` works same as a `*` but it only matches one character in the file's name.  
```
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{sSrPtw9IwORLHN6Pe5Qm8VcTfuK.dJjM4QDLyIzN0czW}
```

### 3. Matching with []  
The square brackes [] are a limited form of ?, in which instead of matching any character, [] 
is used as a subset of characters that are specified within the brackets.  
For eg echo file_[xy] will print the files names with letter x and y after it, file_x and file_y.  
Here we need to print the files by changing the directory first and then running the program in a single argument.  
```
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[bash]
You got it! Here is your flag!
pwn.college{snQS5zQRcDxH3mdUunRlhQIq-a5.dRjM4QDLyIzN0czW}
```

### 4. Matching paths with []  
It is the same as previous code.  
```
hacker@globbing~matching-paths-with-:~$ /challenge/run  /challenge/files/file_[bash]
You got it! Here is your flag!
pwn.college{snQS5zQRcDxH3mdUunRlhQIq-a5.dRjM4QDLyIzN0czW}
```

### 5. Mixing globs  
Here, we need to display 3 files but by using only 6 characters or less. So we can use the starting letters of challenging, educational and pwning as no other words start with that character.  

```
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ ls
amazing    challenging  educational  great  incredible  kind      magical  optimistic  queenly  splendid   uplifting   wonderful  youthful
beautiful  delightful   fantastic    happy  jovial      laughing  nice     pwning      radiant  thrilling  victorious  xenial     zesty
hacker@globbing~mixing-globs:/challenge/files$ ls [cep]*
challenging  educational  pwning
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run ls[cep]*
Error: your argument is too long! It must be 6 characters or less.

hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{cmv1eT7KiwNZCtBH2UK-QkVn2Wn.dVjM4QDLyIzN0czW}
```

### 6. Exclusionary globbing  
If the first character in the brackets is a ! or (in newer versions of bash) a ^, the glob inverts, and the letters in the bracket matches characters that aren't listed. This helps us to eliminate the words which we don't to print.  
So we first change the directory to /challenge/files and then in a single argument print the words not starting with p, w, or n.  

```
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ 
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [!pwn]*
You got it! Here is your flag!
pwn.college{QWtRGL8eNUP-a52L_Frrd0MeJvF.dZjM4QDLyIzN0czW}
```
