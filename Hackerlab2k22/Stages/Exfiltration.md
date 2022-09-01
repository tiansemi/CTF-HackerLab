#  Exfiltration
```
Level: Medium, 300pts 
```

# Description: 
```
A conversation between two terrorist groups has been intercepted. It is possible that very sensitive data was transmitted during the communication.

Flag : CTF_*

```

>For this challenge, we are given an PCAP file capture.pcap 
PCAP file contains a recorded conversation between a DNS client and a server, where DNS queries and CNAME responses seem to contain encoded messages:

>We can filter the cname queries with tshark 

`$ tshark -r capture.pcap -T fields -e dns.qry.name`

We wrote a python code to exfiltrate the data  

>We get two files. An image file and a zip file 
on the image file it is written rockyou ft leet. So we thought we have to crack the zip password with john using rockyou.txt but nothing. 
So we made a bruteforce 

`$ zip2john a.zip > hashes.txt `

john hashes.txt 
