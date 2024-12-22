# Forensics  

## Trivial Flag Transfer Protocol  
<img width="442" alt="image" src="https://github.com/user-attachments/assets/bc6d96be-1622-48c8-8cb8-1a9d37162145" />  

This challenge required a lot of tools and techniques. This was my first Forensics challenge, hence referred to many 
articles like https://trailofbits.github.io/ctf/forensics/ and tools like binwalk, file command, scalpel, etc, which are widely used for file carving.  
>**File carving** is a data technique used for recovering any data in order to extract files from raw data, mostly without relying on filesystem metadata.

Since on seeing the file, it came out to be `pcapng` one, I got to know about the usage of the **Wireshark** tool to handle files. Now,  
>A **PCAPNG (Packet CAPture Next Generation)** file is a newer format for _storing network traffic captures_. It’s an extended version of the older PCAP format
>and allows more flexibility, including support for multiple interfaces, packet metadata, and more detailed timestamps. Common tools for analysing them are Wireshark, `tcpdump`,etc.  

First I tried using Wireshark via WSL, but it kept showing this message even after installing all libraries.   
`wireshark: error while loading shared libraries: libQt5Core.so.5: cannot open shared object file: No such file or directory`  

So installed the app on desktop itself and opened the tftp file. Learnt about a few feature from https://www.comptia.org/content/articles/what-is-wireshark-and-how-to-use-it.    
<img width="960" alt="image" src="https://github.com/user-attachments/assets/e1b6a7aa-6163-4b98-a1ae-1b961d75f497" />  

This showed a huge list of files with their timestamps, source, destination ip addresses, protocols, info etc. Since I wanted to work with tftp type files with data in it, 
I filtered them using tftp.type command. This allowed me to see only the useful ones.  
<img width="960" alt="image" src="https://github.com/user-attachments/assets/5d0c01c0-23c3-49b6-8441-c2e083d5be07" />  

Next I went to File tab > Export Objects > TFTP... Then saved all the files in the system to access them.  
![Screenshot (22)](https://github.com/user-attachments/assets/6fdd10ec-4514-41ea-bbc8-f1c46666a08a)   
<img width="556" alt="image" src="https://github.com/user-attachments/assets/eaddddaf-9bb6-4723-8ded-7e1f4d507ea4" />  
<img width="577" alt="image" src="https://github.com/user-attachments/assets/5467a9d7-fa07-44bf-914e-823456635fcc" />  


Now, to check them one by one, started off with `instructions.txt` file that contained the following code:   
```
cat instructions.txt
GSGCQBRFAGRAPELCGBHEGENSSVPFBJRZHFGQVFTHVFRBHESYNTGENAFSRE.SVTHERBHGNJNLGBUVQRGURSYNTNAQVJVYYPURPXONPXSBEGURCYNA
```
This text seemed meaningless at first, but then struck the idea of using **ROT13**. Used https://cryptii.com/pipes/rot13-decoder to decode the following text.  
TFTPDOESNTENCRYPTOURTRAFFICSOWEMUSTDISGUISEOURFLAGTRANSFER.FIGUREOUTAWAYTOHIDETHEFLAGANDIWILLCHECKBACKFORTHEPLAN  
which is TFTP DOESNT ENCRYPT OUR TRAFFIC SO WE MUST DISGUISE OUR FLAG TRANSFER. FIGURE OUT A WAY TO **HIDE THE FLAG** AND I WILL CHECK BACK FOR THE **PLAN**  
Here two terms were meaningful, the flag is hidden as stated in the hint, we might need to use steganographic tools, eg **steghide**.  
>**Steghide** is a steganography program that is able to **hide data** in various kinds of image- and audio-files.  (https://steghide.sourceforge.net/)

Also it stated to check the plan file.  
```
cat ./plan
VHFRQGURCEBTENZNAQUVQVGJVGU-QHRQVYVTRAPR.PURPXBHGGURCUBGBF
```  
Another rot13 text, which was: I USED THE **PROGRAM** AND **HID** IT WITH-**DUE DILIGENCE**. CHECKOUT THE **PHOTOS**  
for checking the program, i tried to install deb type, which showed:  
```
sudo apt-get install ./program.deb
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Note, selecting 'steghide' instead of './program.deb'
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 steghide : Depends: libjpeg62-turbo (>= 1:1.3.1) but it is not installable
E: Unable to correct problems, you have held broken packages.
```
Though it didn't install, it showed a line that stated `Note, selecting 'steghide' instead of './program.deb'`, another hint for using steghide. We can use it to reverse the flag. Visited https://www.geeksforgeeks.org/how-to-install-steghide-tool-in-linux/.  
Syntax for using steghide: **`steghide extract -sf <filename> -p <password>`**
We knew the file name, for password it maybe DUE DILIGENCE as stated in the line.   
```
apt install steghide
steghide extract -sf ./picture1.bmp -p "DUEDILIGENCE"
steghide: could not extract any data with that passphrase!
steghide extract -sf ./picture2.bmp -p "DUEDILIGENCE"
steghide: could not extract any data with that passphrase!
steghide extract -sf ./picture3.bmp -p "DUEDILIGENCE"
the file "flag.txt" does already exist. overwrite ? (y/n) y
wrote extracted data to "flag.txt".  
```

On the first 2 pictures, no data was found, but on the third it showed data extracted, which lead us straight to the file.txt file!  
```
cat flag.txt
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}  
```














