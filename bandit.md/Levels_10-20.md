#Bandit Game  

## Level 10-11  
In this challenge, I just used the `cat` command to get the password encoded in base 64. Then I used an online
base 64 decoder (https://www.base64decode.org/) to get the password.  
```
bandit10@bandit:~$ ls -a
.  ..  .bash_logout  .bashrc  data.txt  .profile
bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
```
The decoded data was:  
```
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

## 
