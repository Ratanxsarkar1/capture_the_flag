
![](../attachments/Forensics-6.png)


```
sudo mount -o loop,offset=$((1140736*512)) disk.img mount
```

```
cd home/ctf-player/Code/killer-chat-app/.git/
```

```
git logs
```
fatal: your current branch 'master' does not have any commits yet

```
This suggested that the repository history was **tampered with or removed**.

Git still stores old commits in the **`.git/objects` database**, even if they are no longer referenced.
```

```
`git fsck --lost-found`  -->  dangling commit 01533f7....  --> parent 2151ef0ccc --> git show 2151ef0ccc
```

![](../attachments/Forensics-7.png)

```
picoCTF{g17_r35cu3_16ac6bf3}
```

---
