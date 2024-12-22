# Reverse Engineering  

## vault-door-3  
<img width="432" alt="image" src="https://github.com/user-attachments/assets/907fee61-753d-4541-a61a-b1f30e47fd6e" />  

The java program was as follows:  
```
import java.util.*;

class VaultDoor3 {
    public static void main(String args[]) {
        VaultDoor3 vaultDoor = new VaultDoor3();
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter vault password: ");
        String userInput = scanner.next();
	String input = userInput.substring("picoCTF{".length(),userInput.length()-1);
	if (vaultDoor.checkPassword(input)) {
	    System.out.println("Access granted.");
	} else {
	    System.out.println("Access denied!");
        }
    }

    // Our security monitoring team has noticed some intrusions on some of the
    // less secure doors. Dr. Evil has asked me specifically to build a stronger
    // vault door to protect his Doomsday plans. I just *know* this door will
    // keep all of those nosy agents out of our business. Mwa ha!
    //
    // -Minion #2671
    public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        char[] buffer = new char[32];
        int i;
        for (i=0; i<8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i<16; i++) {
            buffer[i] = password.charAt(23-i);
        }
        for (; i<32; i+=2) {
            buffer[i] = password.charAt(46-i);
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password.charAt(i);
        }
        String s = new String(buffer);
        return s.equals("jU5t_a_sna_3lpm18g947_u_4_m9r54f");
    }
}
```

Usually in easy challenges of Vault Door, the flag would be simply the one given in the code(eg here jU5t_a_sna_3lpm18g947_u_4_m9r54f), but here we had to 
do some changes in the code.  
If we look at the **for loops**, we can see that the first 7 characters remain same in the flag `jU5t_a_s`.  

After that there are some exchanges in the characters. We find that the characters later on are filled in a reverse order.  
I started making the table, but it was getting too lengthy and tedious. Hence decided to modify the program by taking 
the `jU5t_a_sna_3lpm18g947_u_4_m9r54f` in an array variable named `target`, and then applying all the for loops on it.  
The flag would now be stored in the array `password`.    
```
public class VaultDoor {
    public static void main(String[] args) {
        char[] target = "jU5t_a_sna_3lpm18g947_u_4_m9r54f".toCharArray();
        char[] password = new char[32];

        // Reverse map buffer to password
        for (int i = 0; i < 8; i++) {
            password[i] = target[i];
        }
        for (int i = 8; i < 16; i++) {
            password[23 - i] = target[i];
        }
        for (int i = 16; i < 32; i += 2) {
            password[46 - i] = target[i];
        }
        for (int i = 31; i >= 17; i -= 2) {
            password[i] = target[i];
        }

        System.out.println("picoCTF{" + new String(password) + "}");
    }
}
```  
Finally, printed the flag along with `picoCTF`.  
```
root@DESKTOP-0QGCC7M:/mnt/c/Users/Laptop/Downloads# javac VaultDoor.java
root@DESKTOP-0QGCC7M:/mnt/c/Users/Laptop/Downloads# java VaultDoor
picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_79958f}  
```
Hence, by executing the code, got the flag!  
**`picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_79958f}`**




