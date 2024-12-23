# Cryptography  

## Vigenere  
<img width="437" alt="image" src="https://github.com/user-attachments/assets/230531b9-996b-4348-8813-219a4b9fa093" />  

The cipher given to me was `rgnoDVD{O0NU_WQ3_G1G3O3T3_A1AH3S_2951c89f}`.  
This clearly indicated that we can get the flag by using vigenere cipher rotation.  

>The **Vigenère cipher** is a method of encrypting alphabetic text where each letter of the plaintext is encoded
> with a different **Caesar cipher**, whose increment is determined by the corresponding letter of another text,
>the **key**.
>Hence, it can be differentiated from the Caeser cipher, as in that the all alphabets were incremented by a fixed no.

>The main part of breaking a Vigenere Cipher is the key itself. Because it repeats,
>it's vulnerable to attacks like **brute forcing** the rotation by figuring out the **length of the key**.
>After, frequency analysis or key elimination is used to reverse the secret.

Studied some resources like https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher and https://ctf101.org/cryptography/what-is-a-vigenere-cipher/ 
for basics.  

Used this [tool](https://cryptii.com/pipes/rot13-decoder) to get the right flag by entering the key given in the 
description `CYLAB`.  
<img width="935" alt="image" src="https://github.com/user-attachments/assets/25a553ee-8964-4a5b-9603-920e70eaf5df" />  

Hence the flag was  
**`picoCTF{D0NT_US3_V1G3N3R3_C1PH3R_2951a89h}`**


