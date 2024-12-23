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

So if the key here is `CYLAB`, then the key for the whole message `rgnoDVD{O0NU_WQ3_G1G3O3T3_A1AH3S_2951c89f}` becomes like `CYLABCYLABCYLABCYLABCYLABCYLABCYLABCYL`, as it repeats itself till the end letter of the message.  
So by using the **Vigenere's decryption formula**  
<img width="163" alt="image" src="https://github.com/user-attachments/assets/1a9e7ca6-9178-46e5-b1de-72330e703e28" />  
, where `Pi` is the position of plaintext(the result we want),  
`Ci` is the position of ciphertext(the message given to us), and  
`Ki` is the position of letter from the key.  
`mod 26` ensures that the result stays from A to Z only.  

Substituing our values, eg:  
C1= pos of r, which is 18  
K1= pos of c, which is 3,  
we get the position of P1 as 15, which corresponds to **p**.  
The cases remain same as mentioned in the message.  

---

Used this [tool](https://cryptii.com/pipes/rot13-decoder) to get the right flag by entering the key given in the 
description `CYLAB`.  
<img width="935" alt="image" src="https://github.com/user-attachments/assets/25a553ee-8964-4a5b-9603-920e70eaf5df" />  

Hence the flag was  
**`picoCTF{D0NT_US3_V1G3N3R3_C1PH3R_2951a89h}`**


