

#  Ecowas Portal

```
Level: Basic, 50pts 
```

# Description: 

<img src="File/ecowas1.png">

>To challenge it is a reverse engineering, we will start by observing the code with Ghidra.

<img src="File/ecowas2.png">

>We find several variables in the main which seems to be our flag.When we go through the code a little we notice that the flag is 25 characters which corresponds to the number of variables that we had previously seen. We must then determine which method was used to encrypt the contents of these variables.

<img src="File/ecowas3.png">

>We then come across the encrypt function which seems to be the encryption method to use.
>By reading the contents of the function we can see that the function receives two parameters, one which corresponds to a character of the flag and another which corresponds to the index of the character. Then we notice that the function subtracts 0x14 (20) from our first parameter then it makes an xor of the result with the index of this character which corresponds to the second parameter. 

<img src="File/ecowas4.png">

>Once we understood that, we just had to write a python code to do the opposite of the function.

<img src="File/ecowas5.png">

>When we execute the script we get our flag

<img src="File/ecowas6.png">

>```Flag :``` **CTF_b451Cr3V0438032832012**
