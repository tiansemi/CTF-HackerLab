# Secret Doc
```
Level: Basic, 30pts
```
# Description
```
Does the content look familiar?
Flag : CTF_*
```

>For this challenge, the name already gives us a hint, `secret`. 
>Indeed, when trying to open it, we have a nice prompt that asks us for the password.
>lmao, we don't have it. It will take a brute force.

>We used two tools, which are: `john` and `hashcat`.
>The first thing we need to do is extract the hash of our password-protected docx file.
>Run the following command and pipe the output into "hash.txt" for later use.

`$ python office2john.py secret.docx > hash.txt`

>We can see now the hash that I saved.

`# cat hash.txt`
```
$office$*2013*100000*256*16*744b3976099db961c0b732b3cf844f6b*316c99e8ab8e5b972714d9e8f289f808*09b4dcc218db1d0590a9609ffeb3d1e08bcc10dca254a958b40b018d07ac5670
```

>Now that we have our hash, we can break it with hashcat.

`$ hashcat -a 0 -m 9600 --force hash.txt rockyou.txt`
>The -a flag sets the attack type as the default straight mode of 0.


>The -m flag specifies the mode we want to use, 9600 for the `MS office Documents`

>After a few minutes of waiting, we have our password to open the document 🥳. And the password is `H4cK3r` youpiiiii. 
>Wait 😩 itsn't yet the end xD. We then have a text that means nothing at a glance: `DSAXC7D.`. After few minutes of thinking, Copy All(Ctrl+a) and past in our preferate text editor give us this `DSAXC7D.86543Eur04&&`. 
>But what is this type of encryption ? 🤔. `XOR` perhaps. We already know the output format of the flag. `CTF_`

>Let's try to find the XOR key that encode it. We did it in python.

`python3 -c "for i,j in zip(list('CTF_'),list('DSAX')): print(ord(i)^ord(j))"`
>The result is 7 for the four caracters. What's the conclusion?. `7` is the key for the XOR encryption.
>Let decode it.

`$ python3 -c "for i in 'DSAXC7D.86543Eur04&&': print(chr(ord(i)^7),end='')"`

Finally we got our flag: ```CTF_D0C)?1234Bru73!!```
