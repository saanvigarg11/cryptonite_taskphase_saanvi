# Cryptography  

## miniRSA  
<img width="437" alt="image" src="https://github.com/user-attachments/assets/ccd125f9-b45e-4fec-89d2-ecb38a813094" />  

The file contained the following values:  
```
N: 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673
e: 3

ciphertext (c): 2205316413931134031074603746928247799030155221252519872650080519263755075355825243327515211479747536697517688468095325517209911688684309894900992899707504087647575997847717180766377832435022794675332132906451858990782325436498952049751141 
```

After referring to these sites, https://ctf101.org/cryptography/what-is-rsa/ and https://en.wikipedia.org/wiki/RSA_(cryptosystem)  
got to know few basic terms about RSA.  
> **RSA (Rivest–Shamir–Adleman)**(kept after its authors) is a public-key cryptosystem, which is one of those oldest widely used for **secure data transmission**.  
> It mainly has 2 keys:    
>**Public Key**: Used for encryption and is shared with everyone.  
>**Private Key**: Used for decryption and is kept secret.  
>
>  An RSA user creates and publishes a public key based on **two large prime numbers**, along with an
> auxiliary value. _The prime numbers are kept secret_. Messages can be encrypted by anyone, via the public key, but can only be decrypted by
> someone who knows the **private key**.

Now, the symbols that are used to denote various numbers and data include:  
>**m**: represents the **message**  which is converted into a no.
>**n**: the **modulus and its length** in bits is the bit length.  
>**c**: represnts the encrypted message or **ciphertext**.    
>**p** and **q**: are **prime numbers** which make up `n`. (`n = pq`)     
>**e**: is the public exponent.    
>**d**: is the private exponent.

Coming to the calculations part,   
<img width="155" alt="image" src="https://github.com/user-attachments/assets/51433db5-f1f6-4537-9307-e0189b3e6ceb" />    
However, when given only e and n, it is extremely difficult to find d.(as its private)  

Approaching the problem now, as the hint stated, we can't approximate the numbers. So I went forward a Python program for doing **binary search** and then do the calculation part.  
```
def integer_nth_root(x, n):
    """Find the integer nth root of x."""
    low, high = 0, x
    while low < high:
        mid = (low + high + 1) // 2
        if mid**n > x:
            high = mid - 1
        else:
            low = mid
    return low

# Inputs
N = 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705
e = 3
c = 2205316413931134031074603746928247799030155221252519872650080519263755075355825243327515211479747536697517688468095325517209911688684309894900992899707504087647575997847717180766377832435022794675332132906451858990782325436498952049751141 

# Computing the integer cube root of c
M = integer_nth_root(c, e)

# the result
if M**e == c:
    print(f"Decrypted plaintext (exact root): {M}")
```

RSA is done in 3 steps:  
-**Key Generation** (_We are already given the values so we need not worry about this._)    
-**Encryption**  
-**Decryption**  

The function `integer_nth_root` computes the integer n-th root of a given number x. I ran a binary search to calculate this integer root.  
It works for large numbers without any need of external libraries.

Our goal is to calculate the original message `M` from the ciphertext(`c`). Since the RSA encryption is `c = M^e mod N`, where `e=3`, we are trying to calculate the integer cube root of `c` to recover the message `M`.   
`M = integer_nth_root(c, e)`   

The final step is to verify that it is the correct plaintext by checking if:  
`M**e == c`  
If it does, this will print the decrypted message.  

On running the code, got this message.  
```
root@DESKTOP-0QGCC7M:/mnt/c/Users/Laptop/Downloads# python3 rsa.py
Decrypted plaintext (exact root): 13016382529449106065894479374027604750406953699090365388203722801043052339225981  
```

Converting this to **hexadecimal** form using python, i got:  
```
>>>hex(13016382529449106065894479374027604750406953699090365388203722801043052339225981)
'0x7069636f4354467b6e3333645f615f6c41726733725f655f64306364366561657d'
```

It seemed that the flag can be reached by changing this form to **ASCII or text** form.    
Using this [tool](https://www.rapidtables.com/convert/number/hex-to-ascii.html), got the following flag!  
<img width="464" alt="image" src="https://github.com/user-attachments/assets/8914f78b-2585-46b8-9a61-e819828b10d2" />    

**`picoCTF{n33d_a_lArg3r_e_d0cd6eae}`**











