
![](../attachments/Forensics-3.png)
## List all files (including deleted)

Run:

`fls -rd disko-4.dd`

Options:
- `-r` → recursive
- `-d` → show deleted files
Deleted files will appear like:

`r/r * 1234: FLAG.TXT`
The `*` means **deleted file**.

```
fls -rd disko-4.dd
r/r * 522629:	log/messages
r/r * 532021:	log/dont-delete.gz

```

```
icat disko-4.dd 532021 > dont-delete.gz
```

```
gunzip dont-delete.gz
cat dont-delete 
	Here is your flag
	picoCTF{d3l_d0n7_h1d3_w3ll_fe34c2cb}

```

```
picoCTF{d3l_d0n7_h1d3_w3ll_fe34c2cb}
```

---
