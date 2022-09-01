#  Exfiltration
```
Level: Medium, Forensic, 300pts 
```

# Description: 
```
A conversation between two terrorist groups has been intercepted. It is possible that very sensitive data was transmitted during the communication.

Flag : CTF_*

```

>For this challenge, we are given an PCAP file capture.pcap 
PCAP file contains a recorded conversation between a DNS client and a server, where DNS queries and CNAME responses seem to contain encoded messages:

>We can filter the A queries with tshark 

`$ tshark -r capture.pcap -Y "dns.qry.type == 1" -T fields -e dns.qry.name | uniq | cut -d"." -f 1 | xxd -r -p  > file1`



>So we do 

`$file file1`
```
file1: PNG image data, 757 x 459, 8-bit/color RGB, non-interlaced
```


 > filter the type cname queries with tshark 
 
`$ tshark -r capture.pcap -Y "dns.qry.type == 5" -T fields -e dns.qry.name | uniq | cut -d"." -f 1 | xxd -r -p  > file2`

`$file file2`
```
file2: Zip archive data, at least v2.0 to extract, compression method=deflate
```

Arrived at this level it is needed:
* decompress the zip file n times with unzip to get a bzip2 file  
* decompress the bzip2 file n times by doing bzip2 -d to get a gzip file 
* decompress the gzip file n times by doing gzip -d to get a zip file which is password protected 

>Honestly, it was a fastidious and useless job.  
So in the end we get two files. An image file and a password protected zip file  
on the image file it says rockyou ft leet. So we thought we should crack the zip password with john using rockyou.txt but nothing yet a prank from the organizers. 

>So we made a bruteforce 

`$ zip2john a.zip > hashes.txt `

`$ john hashes.txt` 

>After a few minutes we get the password of the file 😎 : **3c0w45** 
We obtain our file flag.txt inside there is a code qr written with #. So we just have to scan the code to get the flag 

```Flag:``` **CTF_W3lc0Me_h4CKER5_338333371819**
