# Linux Luminarium  
## Comprehending Commands  

### 1. cat: not the pet, but the command!  
**cat** commands is used to concatenate or jon two or more multiple files.  
In this we have to copy flag file using cat command.  
```
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{8YDGsplueGKdpD6mW3kiXktBQm6.dFzN1QDLyIzN0czW}
```

### 2. Catting absolute paths  
We can also copy the arguments of cat as **absolute paths**. This time, we need to specify the absolute path, 
with cat, i.e. `/flag` to read the file.  
```
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{MaH1BvLBuFxe4gezjXp3NPPDIwf.dlTM5QDLyIzN0czW}
```

### 3. more catting practice  
It uses the same concept as above. We need to put the argument as an absolute path, that is given in the description.
`/usr/share/bug/flag` without using cd command.  
```
You cannot use the 'cd' command in this level, and must retrieve the flag by 
absolute path. Plus, I hid the flag in a different directory! You can find it 
in the file /usr/share/bug/flag. Go cat it out **without** cding into that 
directory!
hacker@commands~more-catting-practice:~$ cat /usr/share/bug/flag
pwn.college{w2GsTwbUmzhLtXfVUlHCbUaB4RE.dBjM5QDLyIzN0czW}
```

### 4. grepping for a needle in a haystack  
The `grep` command is used to **search for a text** in a very large file. It is used when we want to cat files
which are really big.   
The syntax is `grep SEARCH_STRING /path/to/file`.  
In this we have to search for a flag starting with **pwn.college**, so it will come in place of SEARCH_STRING. And the path is 
**/challenge/data.txt**.  
```
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{UXVSOMZEf2f7wwtzV0osp3rWbTt.ddTM4QDLyIzN0czW}
```

### 5. listing files  
`ls` command is used to **list all the contents** of a directory. If we don't specify any argument, it will list all the contents in the 
current directory.  
In this we put an argument /challenge to know its contents.  
```
hacker@commands~listing-files:~$ ls /challenge
20975-renamed-run-21007  DESCRIPTION.md
hacker@commands~listing-files:/challenge$ /challenge/20975-renamed-run-21007
Yahaha, you found me! Here is your flag:
pwn.college{8qSEXb5SFhWH7OGTiv0301zO46T.dhjM4QDLyIzN0czW}
```

### 6. touch command  
`touch` command is used to **create new files** in any directory. We can either create the files in our home hacker or in any other directory
by using the cd command.  
Here, we need to create two file named pwn and college in tmp directory.  
```
hacker@commands~touching-files:~$ cd /tmp
hacker@commands~touching-files:/tmp$ touch pwn
hacker@commands~touching-files:/tmp$ touch college
hacker@commands~touching-files:/tmp$ ls
bin      hsperfdata_root  tmp.MiOQGWw5Zc              vscode-ipc-68808be3-6ee9-4c97-a459-7b0808542707.sock
college  pwn              vscode-git-f752b1f444.sock  vscode-ipc-d337146b-8e9c-4dc6-9102-9fdc3b3456a6.sock
hacker@commands~touching-files:/tmp$ /challenge/run
Success! Here is your flag:
pwn.college{49n3FUqd0oGbBynvuRF_keKDIH8.dBzM4QDLyIzN0czW}
```

### 7. removing files  
`rm` command is used to **remove any file** from a directory.   
Here, we are given a `delete_me` file which we need to delete.  
```hacker@commands~removing-files:~$ ls
Desktop  a  delete_me
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ ls
Desktop  a
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{oco8ffFQ_YTb0LMkS4W3CuP9f_a.dZTOwUDLyIzN0czW}
```

### 8. hidden files  
Since `ls` command doesn't list all the files in the directory, we need to use ls -a to list the hidden files.  
In the desc, its given that the directory is /, so we changed the directory and then executed `ls -a` command. There we found the flag
but to get it, we need to use the cat command.  
```
hacker@commands~hidden-files:~$ ls
Desktop  a
hacker@commands~hidden-files:~$ ls -a
.  ..  .ICEauthority  .bash_history  .bash_logout  .bashrc  .cache  .config  .dbus  .local  .md  .profile  Desktop  a
hacker@commands~hidden-files:~$ /challenge/run
There's no flag here for you! I made the flag readable but hid it as a .-prepended file in the / directory. Go find it!
hacker@commands~hidden-files:~$ cd /
hacker@commands~hidden-files:/$ ls -a
.   .dockerenv          bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
..  .flag-376269024800  boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~hidden-files:/$ cat .flag-376269024800
pwn.college{kXkwIiR1KADHanAbuR_H0AfhiOs.dBTN4QDLyIzN0czW}
```

### 9. An Epic Filesystem Quest  
In this challenge, we need to make alternate uses of `cd`, `ls` and `cat` functions wherever required as per clue.  

hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls
BLUEPRINT  boot       dev  flag  lib    lib64   media  nix  proc  run   srv  tmp  var
bin        challenge  etc  home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~an-epic-filesystem-quest:/$ cat BLUEPRINT
Lucky listing!
The next clue is in: /opt/aflplusplus/nyx_mode/libnyx/libnyx

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/$ cd /opt/aflplusplus/nyx_mode/libnyx/libnyx
hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/libnyx/libnyx$ ls -a
.  ..  .BRIEF  .gitignore  Cargo.lock  Cargo.toml  build.rs  cbindgen.toml  libnyx.h  src  target  test.c  test.sh
hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/libnyx/libnyx$ cat .BRIEF
Great sleuthing!
The next clue is in: /opt/linux/linux-5.4/include/trace/events

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!

hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/libnyx/libnyx$ ls /opt/linux/linux-5.4/include/trace/events
9p.h                f2fs.h               iocost.h      net.h                rpcrdma.h   tegra_apb_dma.h
TIP-TRAPPED         

hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/libnyx/libnyx$ cat Great sleuthing!
The next clue is in: /opt/linux/linux-5.4/include/trace/events                    ls /opt/linux/linux-5.4/include/trace/events
                                                                                  cd /
hacker@commands~an-epic-filesystem-quest:/$ cd /opt/aflplusplus/nyx_mode/libnyx/libnyx
hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/libnyx/libnyx$ ls -a
.  ..  .BRIEF  .gitignore  Cargo.lock  Cargo.toml  build.rs  cbindgen.toml  libnyx.h  src  target  test.c  test.sh
hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/libnyx/libnyx$ cat .BRIEF
Great sleuthing!
The next clue is in: /opt/linux/linux-5.4/include/trace/events

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/libnyx/libnyx$ ls /opt/linux/linux-5.4/include/trace/events
9p.h                f2fs.h               iocost.h      net.h                rpcrdma.h   tegra_apb_dma.h
TIP-TRAPPED         fib.h      
hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/libnyx/libnyx$ cat /opt/linux/linux-5.4/include/trace/events/TIP-TRAPPED
Yahaha, you found me!
The next clue is in: /opt/angr-management/_internal/PySide6/Qt/qml/QtTextToSpeech

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/libnyx/libnyx$ ls /opt/angr-management/_internal/PySide6/Qt/qml/QtTextToSpeech
POINTER-TRAPPED  libtexttospeechqmlplugin.so  plugins.qmltypes  qmldir
hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/libnyx/libnyx$ cat /opt/angr-management/_internal/PySide6/Qt/qml/QtTextToSpeech/POINTER-TRAPPED
Tubular find!
The next clue is in: /opt/aflplusplus/.git/modules/nyx_mode/packer/logs/refs/remotes/origin
hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/libnyx/libnyx$ ls /opt/aflplusplus/.git/modules/nyx_mode/packer/logs/refs/remotes/origin
HEAD  NUGGET

hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/libnyx/libnyx$ cat /opt/aflplusplus/.git/modules/nyx_mode/packer/logs/refs/remotes/origin/HEAD
0000000000000000000000000000000000000000 bcf3e248b660764f48af54232a3388389a2dfc22 root <root@buildkitsandbox.(none)> 1725641028 +0000   clone: from https://github.com/nyx-fuzz/packer.git
hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/libnyx/libnyx$ cat /opt/aflplusplus/.git/modules/nyx_mode/packer/logs/refs/remotes/origin/NUGGET
Yahaha, you found me!
The next clue is in: /opt/pwndbg/.venv/lib/python3.8/site-packages/nacl/bindings

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/libnyx/libnyx$ cd /opt/pwndbg/.venv/lib/python3.8/site-packages/nacl/bindings
hacker@commands~an-epic-filesystem-quest:/opt/pwndbg/.venv/lib/python3.8/site-packages/nacl/bindings$ ls
GIST         crypto_aead.py  crypto_generichash.py  crypto_pwhash.py      crypto_secretstream.py  randombytes.py
__init__.py  crypto_box.py   crypto_hash.py         crypto_scalarmult.py  crypto_shorthash.py     sodium_core.py
__pycache__  crypto_core.py  crypto_kx.py           crypto_secretbox.py   crypto_sign.py          utils.py
hacker@commands~an-epic-filesystem-quest:/opt/pwndbg/.venv/lib/python3.8/site-packages/nacl/bindings$ cat GIST
Tubular find!
The next clue is in: /usr/share/man/fr/man8

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/opt/pwndbg/.venv/lib/python3.8/site-packages/nacl/bindings$ cd /usr/share/man/fr/man8
hacker@commands~an-epic-filesystem-quest:/usr/share/man/fr/man8$ ls -a

hacker@commands~an-epic-filesystem-quest:/usr/share/man/fr/man8$ cat .INSIGHT
Great sleuthing!
The next clue is in: /opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/shellcraft/templates/thumb/android/syscalls
hacker@commands~an-epic-filesystem-quest:/usr/share/man/fr/man8$ cd /opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/shellcraft/templates/thumb/android/syscalls
hacker@commands~an-epic-filesystem-quest:/opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/shellcraft/templates/thumb/android/syscalls$ ls
TRACE
hacker@commands~an-epic-filesystem-quest:/opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/shellcraft/templates/thumb/android/syscalls$ cat TRACE 
Congratulations, you found the clue!
The next clue is in: /opt/linux/linux-5.4/sound/soc/sh/rcar

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/shellcraft/templates/thumb/android/syscalls$ cd /opt
/linux/linux-5.4/sound/soc/sh/rcar
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/sound/soc/sh/rcar$ ls
LEAD  Makefile  adg.c  cmd.c  core.c  ctu.c  dma.c  dvc.c  gen.c  mix.c  rsnd.h  src.c  ssi.c  ssiu.c
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/sound/soc/sh/rcar$ cat LEAD
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{gFo1Uxk4z7gMYnFCgPU5giWKVds.dljM4QDLyIzN0czW}


