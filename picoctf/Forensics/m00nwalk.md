# Forensics  

## m00nwalk  
<img width="433" alt="image" src="https://github.com/user-attachments/assets/ad67f4ee-db61-40b2-b468-2a478b779bc8" />  

It included an audio file(`wav` type) with some sound. As the hint suggested, I went on finding about how images are sent from moon 
to the Earth. This website https://en.wikipedia.org/wiki/Apollo_11_missing_tapes helped in gaining some clue.  

>**SSTV (Slow Scan Television)** is a method of sending and receiving **still images** using **radio frequencies**. 
>Unlike traditional TV, which transmits many frames per second, SSTV transmits **one image frame at a time**,
>typically over amateur **radio**. It’s often used by ham radio operators, as in **space communications**,
>like sending images from the International Space Station (ISS).  
>
>In the website, it talked about the **Apollo 11** missing tapes were those that were recorded from
>Apollo 11's SSTV telecast in its **raw format** on telemetry **data tape** at the time of the **first Moon landing** in 1969 and subsequently lost.
>The **data tapes** were used to record all transmitted data (video as well as telemetry) for backup.  
>
>**Telemetry** is the process of remotely collecting and transmitting data from devices, sensors or systems to a central location for monitoring, analysis, and control.
>Its mostly used in industries such as aerospace, environmental monitoring, etc.


Since we were given an audio message, it gave an idea to decode it into an **image**. For that,  
intially I tried using tools like `qsstv` and `pavucontrol` when i searched through this [article](https://ourcodeworld.com/articles/read/956/how-to-convert-decode-a-slow-scan-television-transmissions-sstv-audio-file-to-images-using-qsstv-in-ubuntu-18-04).  
But in my wsl, it kept showing errors like these even after reinstalling this library `libQt5Core.so.5` and updating, etc.  
```
root@DESKTOP-0QGCC7M:/mnt/c/Users/Laptop/Downloads# qsstv
qsstv: error while loading shared libraries: libQt5Core.so.5: cannot open shared object file: No such file or directory  
root@DESKTOP-0QGCC7M:/mnt/c/Users/Laptop/Downloads# pavucontrol

(pavucontrol:405): Gtk-WARNING **: 20:58:44.536: cannot open display:  
```

So I found some more resources like [this one](https://github.com/colaclanth/sstv/tree/master/sstv) which mentioned the way to convert the file without the use of qsstv, by taking help of 
some Python codes.  
On running the following commands, I finally got the image(`result.png` which got automatically created in my folder) that contained the flag!  
```
root@DESKTOP-0QGCC7M:/mnt/c/Users/Laptop/Downloads# git clone https://github.com/colaclanth/sstv.git
.
.
.
root@DESKTOP-0QGCC7M:/mnt/c/Users/Laptop/Downloads# python setup.py install
.
.
.  
root@DESKTOP-0QGCC7M:/mnt/c/Users/Laptop/Downloads# sstv -d message.wav -o result.png
/usr/local/lib/python3.10/dist-packages/numpy/_core/getlimits.py:551: UserWarning: Signature b'\x00\xd0\xcc\xcc\xcc\xcc\xcc\xcc\xfb\xbf\x00\x00\x00\x00\x00\x00' for <class 'numpy.longdouble'> does not match any known type: falling back to type probe function.
This warnings indicates broken support for the dtype!
  machar = _get_machar(dtype)
[sstv] Searching for calibration header... Found!
[sstv] Detected SSTV mode Scottie 1
[sstv] Decoding image...   [######################################################################################] 100%
[sstv] Drawing image data...
[sstv] ...Done!  
```
The Python code of `setup.py` was:  
```
from setuptools import setup

with open("README.md", "r") as readme:
    long_description = readme.read()

setup(name="sstv",
      version="0.1",
      description="SSTV audio file decoder",
      long_description=long_description,
      long_description_content_type="text/markdown",
      url="http://github.com/colaclanth/sstv",
      author="colaclanth",
      author_email="nomail@c0l.me",
      license="GPLv3",
      packages=["sstv"],
      keywords="sstv decode",
      entry_points={"console_scripts": ["sstv=sstv.__main__:main"]},
      install_requires=[
          'numpy',
          'Pillow',
          'PySoundFile',
          'scipy'
      ],
      classifiers=[
          'License :: OSI Approved :: GNU General Public License v3 (GPLv3)',
          'Programming Language :: Python :: 3',
      ])

!
```
![result](https://github.com/user-attachments/assets/1fa41936-8f2e-42cd-a5ad-34cc7ecb54e9)   


This was the image that contained the flag:  
**`picoCTF{beep_boop_im_in_space}`** 








