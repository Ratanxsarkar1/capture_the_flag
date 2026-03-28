
![](attachments/General%20Skills.png)

![](attachments/General%20Skills-1.png)

![](attachments/General%20Skills-2.png)

```
 nmap -p 55644 mysterious-sea.picoctf.net
Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-03-10 20:29 IST
Nmap scan report for mysterious-sea.picoctf.net (3.130.79.223)
Host is up (0.33s latency).
Other addresses for mysterious-sea.picoctf.net (not scanned): 64:ff9b::382:4fdf
rDNS record for 3.130.79.223: ec2-3-130-79-223.us-east-2.compute.amazonaws.com

PORT      STATE SERVICE
55644/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 1.59 seconds
ghost@morningstar:~$ nmap -p 55644 -A mysterious-sea.picoctf.net
Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-03-10 20:30 IST
Nmap scan report for mysterious-sea.picoctf.net (3.130.79.223)
Host is up (0.26s latency).
Other addresses for mysterious-sea.picoctf.net (not scanned): 64:ff9b::382:4fdf
rDNS record for 3.130.79.223: ec2-3-130-79-223.us-east-2.compute.amazonaws.com

PORT      STATE SERVICE     VERSION
55644/tcp open  netbios-ssn Samba smbd 4.6.2

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 59.97 seconds
ghost@morningstar:~$ smbclient -L mysterious-sea.picoctf.net -p 55644 -N

	Sharename       Type      Comment
	---------       ----      -------
	shares          Disk      Public Share With Guests
	IPC$            IPC       IPC Service (Samba 4.19.5-Ubuntu)
SMB1 disabled -- no workgroup available
ghost@morningstar:~$ smbclient //mysterious-sea.picoctf.net/shares -p 55644 -N
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Sat Mar  7 01:55:43 2026
  ..                                  D        0  Sat Mar  7 01:55:43 2026
  dummy.txt                           N     1142  Thu Feb  5 02:52:17 2026
  flag.txt                            N       37  Sat Mar  7 01:55:43 2026
get
		65536 blocks of size 1024. 58696 blocks available
smb: \> get flag.txt
getting file \flag.txt of size 37 as flag.txt (0.0 KiloBytes/sec) (average 0.0 KiloBytes/sec)
smb: \> 

```

cat flag.txt
```
picoCTF{5mb_pr1nter_5h4re5_8a0df8e0}
```

---
