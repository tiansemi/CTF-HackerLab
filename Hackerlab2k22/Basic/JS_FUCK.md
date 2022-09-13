

# JS Fuck
```
Level: Basic, 10pts 
```

# DESCRIPTION:

<img src="File/js.png">

>This challenge gives us a link to the competition webpage. Referring to the name of the challenge, we decided to look for the js files that are on the website by looking in the source code.

<img src="File/js1.png">

>Looking at the content of js files we come across something interesting in the awesome-fonts.js file. It's js fuck(**JSFuck is an esoteric and educational programming style based on the atomic parts of JavaScript. It uses only six different characters to write and execute code.**)

<img src="File/js2.png">

>We then use the site **https://tio.run/#javascript-node** to decode the content.

<img src="File/js3.png">

>Once we have decoded it does not take long to understand that each element of cipher is xored with the corresponding index. We then write a code in python to obtain the flag.

```python
#!/usr/bin/python3

cipher = [67, 85, 68, 92, 55, 49, 51, 94, 90, 56, 109, 99, 59, 50, 63, 61, 35, 37]
flag=[]
for i in range(len(cipher)):
    flag.append(chr(cipher[i] ^ i))

print(''.join(flag))

```
>Or in js
```
cipher = [67, 85, 68, 92, 55, 49, 51, 94, 90, 56, 109, 99, 59, 50, 63, 61, 35, 37] 
flag = ''
function xor_xor(x,y){ return x ^ y; }

for (var i=0; i < cipher.length ; i++){ 
	flag += String.fromCharCode(xor_xor(cipher[i] ^ i));
}
console.log("The flag is",flag);

```

>By executing our code we get the flag

<img src="File/js5.png">

>```Flag :``` **CTF_345YR1gh7?1234**
