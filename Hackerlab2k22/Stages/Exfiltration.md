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

Nous abtenons deux fichiers. Un fichier image et un fichier zip 

sur le fichier image il est écris rockyou ft leet. Nous avons donc penser qu'il faut cracker le mot de passe zip avec john en utilisant rockyou.txt mais rien. 
On a donc faire un bruteforce 

`$ zip2john a.zip > hashes.txt `

john hashes.txt 
