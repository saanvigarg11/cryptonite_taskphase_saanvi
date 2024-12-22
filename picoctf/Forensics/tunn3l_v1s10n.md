# Forensics  

## tunn3l v1s10n  
<img width="439" alt="image" src="https://github.com/user-attachments/assets/33ebf58c-09b4-483b-a7d9-a3a6054cc531" />  

The file content looked somewhat like this:  
<img width="836" alt="image" src="https://github.com/user-attachments/assets/a72b6351-ae20-4a8e-8aef-3af173561826" />  

Everything was mostly unreadable, so I used the **exiftool** to determine the file specifications, and most importantly the type 
of the file. Got to know from the site https://trailofbits.github.io/ctf/forensics/index.html.   
<img width="572" alt="image" src="https://github.com/user-attachments/assets/57cd74df-dedc-44ad-9fb4-893587255596" />  

```
apt install libimage-exiftool-perl
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
.
.
.
exiftool tunn3l_v1s10n
ExifTool Version Number         : 12.40
File Name                       : tunn3l_v1s10n
Directory                       : .
File Size                       : 2.8 MiB
File Modification Date/Time     : 2024:12:19 18:45:06+05:30
File Access Date/Time           : 2024:12:22 20:27:57+05:30
File Inode Change Date/Time     : 2024:12:19 18:46:11+05:30
File Permissions                : -rwxrwxrwx
File Type                       : BMP
File Type Extension             : bmp
MIME Type                       : image/bmp
BMP Version                     : Unknown (53434)
Image Width                     : 1134
Image Height                    : 306
Planes                          : 1
Bit Depth                       : 24
Compression                     : None
Image Length                    : 2893400
Pixels Per Meter X              : 5669
Pixels Per Meter Y              : 5669
Num Colors                      : Use BitDepth
Num Important Colors            : All
Red Mask                        : 0x27171a23
Green Mask                      : 0x20291b1e
Blue Mask                       : 0x1e212a1d
Alpha Mask                      : 0x311a1d26
Color Space                     : Unknown (,5%()
Rendering Intent                : Unknown (826103054)
Image Size                      : 1134x306
Megapixels                      : 0.347
```
Using this, we get to know the file type, which is **`BMP`**. This gave a clear idea that its an **image**. So I used https://image-viewer.com/#google_vignette website 
to view the image from the file. It looked like this:  
![image](https://github.com/user-attachments/assets/1fc7b81d-f21e-4dd6-b13b-d38bb788e58d)   

So I thought maybe the flag is present in this image only but since that's hidden, I tried to make use of the steghide tool.  
steghide extract -sf ./tunn3l_v1s10n
```
Enter passphrase:
steghide: the bmp file "./tunn3l_v1s10n" has a format that is not supported (biSize: 53434).
This feature is not (yet) available. Please let me (shetzl@chello.at) know
that you want to use this functionality to increase the chance that this will
be implemented in the near future. Steghide has to exit now. Sorry.
```

This wouldn't work, so next I thought of changing the **Contrast/Saturation/Luminance** etc, but that also wouldn't work.  
Then I tried the approach of `hexdump`. Maybe we need to change the dimensions of the image as it somewhat looked like cropped.  
I made use of **CyberChef** (https://gchq.github.io/CyberChef/#recipe=To_Hexdump(16,false,false,false)), a tool which i have been using since the start of CTFs.  
<img width="765" alt="image" src="https://github.com/user-attachments/assets/d5295138-8a74-40bd-8d4c-37fa642cc945" />  

On changing some dimensions, making 01 to 03, and then downloading the new file, we get to see the full image.  
![image](https://github.com/user-attachments/assets/305fe028-6405-4201-9164-e2a67ccc1966)  

Hence the flag is:  
**`picoCTF{qu1t3_a_v13w_2020}`**










