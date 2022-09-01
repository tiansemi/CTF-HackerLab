# 2- Break me

```
Medium: REVERSE, 300pts
```

# Decription
```
Are you able to find the key?
Flag : CTF_*
```

>We have a reverse challenge now. Let's find out what it contains. We will just analyze interesting files.
>The first file: `breakme.py`:
```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import modules.banner as banner
from modules.main import check

if __name__ == '__main__':
    
    banner.banner()

    check(input('Enter the key : '))
```
>Apart from the pretty banner which is imported, we have the check function which is imported from the main file in the module directory.
>Let me show you its contents.
`module/main.py`:
```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import string

def big(data):
    o = ''
    f = (data[-1] + data[:-1])[::-1]
    for i in f:
        o += chr(ord(i) ^ 0xb)
    return o[::2]+ o[1::2]

def bang(data,shift):
    enc = ''
    for c in data:
        if c not in string.ascii_letters:
            enc += c
        else:
            if c in string.ascii_lowercase:
                start = ord('a')
            else:
                start = ord('A')
            enc += chr(((ord(c) - start + shift) % 26) + start)

    return enc[-1] + enc[:-1].swapcase()

def check(s):
    
    if big(bang(bang(big(bang(bang(big(s),18),13)),6),11)) != "ZYYKXWAT[6RM@T6?ES>69=?Z6GRE}6WEGNK^>Oa6" :
        print("\nTry harder :)")
    else:
        print("\nYou got me !")
```
>The check function is the one that checks our flag. We will reverse the line that check our entry : 
` if big(bang(bang(big(bang(bang(big(s),18),13)),6),11)) != "ZYYKXWAT[6RM@T6?ES>69=?Z6GRE}6WEGNK^>Oa6" :`

>This line nests two different functions. `big` and `bang` functions. To solve this challenge, we chose to reverse these two functions. It's not the fastest, but our solution is basically to reverse each statement of these functions.

>Let's call `debig` and `debang` respectively the reverse of big and bang.
>There is our debig function:
```python
def debig(data):
    data=list(data)
    a=data[:20]
    b=data[20:]
    res=''
    temp=''
    for i in range(20):
        temp+=a[i]+b[i]
    for i in temp:
        res+=chr(ord(i)^0xb)
    res=res[::-1]
    res=res[1:]+res[0]
    return res

```
>And there the debang function:
```python
def debang(data,chift):
    data=data[1:].swapcase()+data[0]
    res=''
    M='ABCDEFGHIJKLMNOPQRSTUVWXYZ'
    m='abcdefghijklmnopqrstuvwxyz'
    verif=''
    for c in data:
        if c not in string.ascii_letters:
            res+=c
        else:
            if c in string.ascii_lowercase:
                start = ord('a')
                verif=m
            else:
                start = ord('A')
                verif=M
            for i in verif:
                if ord(c)-start==(ord(i)-start+chift)%26:
                    res+=i
                    break
    return res
            

```

>Now that we have the reverse of the two main functions, we will reverse the check line to get the flag. 
>If calling both functions this way gives us `ZYYKXWAT[6RM@T6?ES>69=?Z6GRE}6WEGNK^>Oa6`, then we have the flag. But we can not guess the flag. Then we must use our reverse function by the same way.
>Let change the check function like this:
```python
def check(s):
    print(debig(debang(debang(debig(debang(debang(debig("ZYYKXWAT[6RM@T6?ES>69=?Z6GRE}6WEGNK^>Oa6"),11),6)),13),18)))
```

>To do this, we started executing the instructions from the outside in. We finished our reverse. Let's now run our file as if nothing had happened.

`$ python3 breakme.py`

>Bammmmmmmm 💥 🔥 we got something :`OBQXG5DFMJUW4LTDN5WS6WRXNAYU24SYGM======`. 

>Ohh zuuuttt 😐 itsn't the flag. Its format is CTF\_*. to make sure we don't have a wrong answer we will revert the initial function check and enter our result.

>There is the result:

<img src="File/image.png">


>So we are on the right way. We will decode this here: <a href="https://gchq.github.io/CyberChef/">CyberChef</a>.

>We will set recipe as magic to identify the encryption.
>It's a pastbin link `pastebin.com/Z7h1MrX3`. Apparently, we are not at the end of our pain yet. 

>The pastbin gives us a blender obj file 😣.
>Let save this in a file to open it online. We found this <a href="https://3dviewer.net">3dviewer</a>

>Yes it seems to be a morse code in 3d view:

<img src="File/model.png">

```-.-. - ..-. ..--.- .-. ...-- ...- ...-- .-. ... . --. ----- ....- --... ..... --... ...-- --. ----- ----. ----. ----. ----. ----.```

>We can decode it on Cyberchef again, and it gives us: `CTF_R3V3RSEG047573G099999`.
>Again this can be the flag, but after fiew minutes of trying we were wrong. Gueesssss, let's change  `0` to `O`. 

>yeahhhh ✅ .

The flag is :`CTF_R3V3RSEG047573G099999`
