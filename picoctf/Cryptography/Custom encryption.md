# Cryptography  

## Custom encryption   
![image](https://github.com/user-attachments/assets/16a2970f-fe05-488e-9d81-61b91a095b22)  
In this challenge, we were given a python code and some input data with cipher text. The python code itself isn't completed
and required some kind of modification. On running the actual code, some error came.  
![image](https://github.com/user-attachments/assets/5b16042d-3a7c-42d6-8a11-1b5522ac9eb8)  

This error occurred because the script expected a command-line argument (sys.argv[1]) for the message,
which we hadn't provided at that time.  

The hint gave an idea to also include **decryption algorithm** by understanding encryption one given in the code.  
Since I hadn't learnt much about the functions in python, I seeked help from some resources like 
https://medium.com/@info_82002/a-beginners-guide-to-encryption-and-decryption-in-python-12d81f6a9eac and about
some definitions from https://www.geeksforgeeks.org/public-key-encryption/?ref=lbp.  
Further i asked chatgpt to also add decrypt algorithm in the actual code wherever encrypt algorithm was given.  
The code was hence changed to:  
```
from random import randint
import sys

def generator(g, x, p):
    return pow(g, x) % p

def encrypt(plaintext, key):
    cipher = []
    for char in plaintext:
        cipher.append(((ord(char) * key * 311)))
    return cipher

def decrypt(cipher, key):
    plaintext = ""
    for num in cipher:
        if num == 0:
            plaintext += "\x00"
        else:
            decrypted_char = num // (key * 311)  
            plaintext += chr(decrypted_char)
    return plaintext

def is_prime(p):
    v = 0
    for i in range(2, p + 1):
        if p % i == 0:
            v = v + 1
    if v > 1:
        return False
    else:
        return True

def dynamic_xor_encrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    return cipher_text

def dynamic_xor_decrypt(ciphertext, text_key):
    plaintext = ""
    key_length = len(text_key)
    for i, char in enumerate(ciphertext):
        key_char = text_key[i % key_length]
        decrypted_char = chr(ord(char) ^ ord(key_char))  
        plaintext = decrypted_char + plaintext 
    return plaintext

def test(plain_text, text_key):
    p = 97
    g = 31
    if not is_prime(p) and not is_prime(g):
        print("Enter prime numbers")
        return
    a = randint(p - 10, p)
    b = randint(g - 10, g)
    print(f"a = {a}")
    print(f"b = {b}")
    u = generator(g, a, p)
    v = generator(g, b, p)
    key = generator(v, a, p)
    b_key = generator(u, b, p)
    shared_key = None
    if key == b_key:
        shared_key = key
    else:
        print("Invalid key")
        return
    semi_cipher = dynamic_xor_encrypt(plain_text, text_key)
    cipher = encrypt(semi_cipher, shared_key)
    print(f'cipher is: {cipher}')

def decode_flag(cipher, text_key, g, p, a, b):

    u = generator(g, a, p)
    v = generator(g, b, p)
    key = generator(v, a, p)
    b_key = generator(u, b, p)

    if key != b_key:
        raise ValueError("Key mismatch during decryption.")

    semi_cipher = decrypt(cipher, key)
    plaintext = dynamic_xor_decrypt(semi_cipher, text_key)

    return plaintext


if __name__ == "__main__":
    if len(sys.argv) > 1:
        message = sys.argv[1]
        text_key = "trudeau"
        test(message, text_key)
    else:
        
        cipher = [97965, 185045, 740180, 946995, 1012305, 21770, 827260, 751065, 718410, 457170, 0, 903455, 228585, 54425, 740180, 0, 239470, 936110, 10885, 674870, 261240, 293895, 65310, 65310, 185045, 65310, 283010, 555135, 348320, 533365, 283010, 76195, 130620, 185045]
        text_key = "trudeau"
        g = 31
        p = 97
        a = 88  
        b = 26  # Value from flag_info

        flag = decode_flag(cipher, text_key, g, p, a, b)
        print(f"{flag}")
```

Here, I added the functions `decrypt` and `dynamic_xor_decrypt`.  
**Plain Text**: It is the message which is readable or understandable. This message is given to the encryption algorithm as an input.  
![image](https://github.com/user-attachments/assets/92e27714-396e-4790-ac15-8c31823159a4)

I assigned the values **88** and **26** to **a** and **b** respectively and the ciphertext as given in the flag_info file, and **p** and **g** were received from the test function which was used for encryption.   

The output hence came was the required flag:  
**`picoCTF{custom_d2cr0pt6d_01.....}`**








