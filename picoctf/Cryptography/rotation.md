# Cryptography  

## rotation  
<img width="434" alt="image" src="https://github.com/user-attachments/assets/22c42434-a058-4241-9adc-4818a30bb965" />  

The text was `xqkwKBN{z0bib1wv_l3kzgxb3l_429in00n}`.  

At first seemed, seemed to just rotate by 13 using ROT13, but it didn't give the required output.  
`kdxjXOA{m0ovo1ji_y3xmtko3y_429va00a}`  

So went on searching some other types of ciphers, which were **substitution**, **caeser**, **Vigenère**. Got to know a lot 
from [here](https://ctf101.org/cryptography/what-is-caesar-cipher-rot-13/).  

>The **Caesar Cipher** or **Caesar Shift** is a cipher that uses the alphabet in order to encode texts.
>Its done to encode each letter with another letter in a **fixed** set of shifts.
>
>**ROT13(Rotate 13)** is a type of Caeser only, just that it has a fixed shift of **13**.
>
> There are only **25** possible "shifts" in the English alphabet.

Using this [decoder](https://cryptii.com/pipes/rot13-decoder) for such operations, I copied the given text, starting from 
7 shifts, it showed this:  
<img width="935" alt="image" src="https://github.com/user-attachments/assets/8f008791-03f2-4003-b2a4-78afcf199193" />  

On increasing the no. of shifts to **8**, I found the correct flag!  
<img width="944" alt="image" src="https://github.com/user-attachments/assets/81dd03e2-7767-4c9e-8bcf-61625f6f2f50" />  

**`picoCTF{r0tat1on_d3crypt3d_429af00f}`**  



