# Linux Luminarium  
## Shell Variables  

### 1. Printing Variables  
This time the flag is put in the variable name FLAG. We can print the variables by using **echo** command
and by putting a **$** sign before the variable name. **$** is used to access variables. This will actually print the path of the file which the variable
stores and hence give the output, that is the flag. The syntax is `echo $<variable_name>`. 
```
hacker@variables~printing-variables:~$ echo $FLAG
pwn.college{sYR9w_IHlzq1AxRsgoQCMeXcmgc.ddTN1QDLyIzN0czW}
```

### 2. Setting Variables  
**=** sign is used to set variables to values. We don't have to put spaces in between while assigning the value to the variable,
(as we do in other languages) as this will try to run the variable instead of assigning any value.  
The syntax is `<variable_name>=<value>`.  

```
hacker@variables~setting-variables:~$ PWN=COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{8E-76eIu9Xq1HJ0D2sFOGSU5IIV.dlTN1QDLyIzN0czW}
```

### 3. Multi-word Variables  
If we want to assign more than 1 word or number or any special character to a variable, we need to put them 
in **single** or **double quotes**. Otherwise, after a space, it will the rest of the characters as commands.  
```
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{Ieg67EaLYTQjN_8bB4NmsJ9ZlEd.dBjN1QDLyIzN0czW}
```

### 4. Exporting Variables  
By default, any other commands that we run in a shell won't run any previous variables of the shell unless we export them, as these
variables are local to that shell. For this we use the `export` command. So when we run the progam, it will print the assigned value
of the variable.  
```
hacker@variables~exporting-variables:~$ export PWN=COLLEGE
You've set the PWN variable to the proper value!
hacker@variables~exporting-variables:~$ COLLEGE=PWN
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ /challenge/run
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great 
job! Here is your flag:
pwn.college{0KbMLYyAlw9zlK0YxcyfddTHfQb.dJjN1QDLyIzN0czW}
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
```

### 5. Printing Exported Variables  
To print exported variables, we can either use `echo` command or **`env`** command. Here, when we use env command, it prints all the
exported variables in the shell. So to find the FLAG, we can use the `grep` command and `|` piping operator.
```
hacker@variables~printing-exported-variables:~$ env
SHELL=/run/dojo/bin/bash
COLORTERM=truecolor
TERM_PROGRAM_VERSION=1.89.1
HOSTNAME=variables~printing-exported-variables
VSCODE_PROXY_URI=https://pwn.college/workspace/code/proxy/{{port}}/
PWD=/home/hacker
DOJO_AUTH_TOKEN=aeca18c0402ccddb62eecde314aa3343ea4c437e0e1e3faad0d009ff8a75f31a
VSCODE_GIT_ASKPASS_NODE=/nix/store/bmmjbvb8hishfrg78ygjlynpq3ikpl39-nodejs-20.15.1/bin/node
HOME=/home/hacker
LANG=C.UTF-8
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=00:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.7z=01;31:*.ace=01;31:*.alz=01;31:*.apk=01;31:*.arc=01;31:*.arj=01;31:*.bz=01;31:*.bz2=01;31:*.cab=01;31:*.cpio=01;31:*.crate=01;31:*.deb=01;31:*.drpm=01;31:*.dwm=01;31:*.dz=01;31:*.ear=01;31:*.egg=01;31:*.esd=01;31:*.gz=01;31:*.jar=01;31:*.lha=01;31:*.lrz=01;31:*.lz=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.lzo=01;31:*.pyz=01;31:*.rar=01;31:*.rpm=01;31:*.rz=01;31:*.sar=01;31:*.swm=01;31:*.t7z=01;31:*.tar=01;31:*.taz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tgz=01;31:*.tlz=01;31:*.txz=01;31:*.tz=01;31:*.tzo=01;31:*.tzst=01;31:*.udeb=01;31:*.war=01;31:*.whl=01;31:*.wim=01;31:*.xz=01;31:*.z=01;31:*.zip=01;31:*.zoo=01;31:*.zst=01;31:*.avif=01;35:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.webp=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:*~=00;90:*#=00;90:*.bak=00;90:*.crdownload=00;90:*.dpkg-dist=00;90:*.dpkg-new=00;90:*.dpkg-old=00;90:*.dpkg-tmp=00;90:*.old=00;90:*.orig=00;90:*.part=00;90:*.rej=00;90:*.rpmnew=00;90:*.rpmorig=00;90:*.rpmsave=00;90:*.swp=00;90:*.tmp=00;90:*.ucf-dist=00;90:*.ucf-new=00;90:*.ucf-old=00;90:
GIT_ASKPASS=/nix/store/3v4hdb2gmpj7jv2z848ikakhzl9rjgwh-code-server/libexec/code-server/lib/vscode/extensions/git/dist/askpass.sh
FLAG=pwn.college{40ureIwaRlwLw9liD7qj5224TGk.dhTN1QDLyIzN0czW}
VSCODE_GIT_ASKPASS_EXTRA_ARGS=
LESSCLOSE=/usr/bin/lesspipe %s %s
TERM=xterm-256color
LESSOPEN=| /usr/bin/lesspipe %s
VSCODE_GIT_IPC_HANDLE=/tmp/vscode-git-decf490978.sock
SHLVL=2
LC_CTYPE=C.UTF-8
VSCODE_GIT_ASKPASS_MAIN=/nix/store/3v4hdb2gmpj7jv2z848ikakhzl9rjgwh-code-server/libexec/code-server/lib/vscode/extensions/git/dist/askpass-main.js
BROWSER=/nix/store/3v4hdb2gmpj7jv2z848ikakhzl9rjgwh-code-server/libexec/code-server/lib/vscode/bin/helpers/browser.sh
PATH=/nix/store/3v4hdb2gmpj7jv2z848ikakhzl9rjgwh-code-server/libexec/code-server/lib/vscode/bin/remote-cli:/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
NODE_EXEC_PATH=/nix/store/bmmjbvb8hishfrg78ygjlynpq3ikpl39-nodejs-20.15.1/bin/node
TERM_PROGRAM=vscode
VSCODE_IPC_HOOK_CLI=/tmp/vscode-ipc-d5d8a667-f26b-404d-a81d-02aa072cf939.sock
_=/run/workspace/bin/env

hacker@variables~printing-exported-variables:~$ env | grep FLAG
FLAG=pwn.college{40ureIwaRlwLw9liD7qj5224TGk.dhTN1QDLyIzN0czW}
```

### 6. Storing Command Output  
To store the output of a command in a variable, we use the **Command Substitution**.  
Syntax: `<variable_name>=$(command)`  
We then use the `echo` command to print the variable.  

```
hacker@variables~storing-command-output:~$ PWN=$(/challenge/run)
Congratulations! You have read the flag into the PWN variable. Now print it out 
and submit it!
hacker@variables~storing-command-output:~$ echo $PWN
pwn.college{wyuDGtM-b0do_wDK-O1VmLjvO8r.dVzN0UDLyIzN0czW}
```

### 7. Reading Input  
We can also ask the user to store a value in the variable. For this we use the **`read`** bulletin and **`-p`** argument to ask for value
from the user. Then we can use the echo command to print the value.  

```
hacker@variables~reading-input:~$ read -p "INPUT:" PWN
INPUT:COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{kEmXe8Z2KI4EUrx79W1obQM7ip1.dhzN1QDLyIzN0czW}
hacker@variables~reading-input:~$
```

### 8. Reading Files  
We can read files directly by using `>` operator, i.e by redirecting files into the input of the command. The syntax is: `read variable < command_name`.  

```
hacker@variables~reading-files:~$ read PWN < /challenge/read_me
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{ElTrdk-ETNMeJ9jH4gEAHpE2c1z.dBjM4QDLyIzN0czW}
```

