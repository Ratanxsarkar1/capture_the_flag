![](attachments/General%20Skills-3.png)


![](attachments/General%20Skills-4.png)

```
cat README.md 
# MyGit

### If you want the flag, make sure to push the flag!

Only flag.txt pushed by ```root:root@picoctf``` will be updated with the flag.

GOOD LUCK!

```

![](attachments/General%20Skills-5.png)


```
git config user.name "root"
ghost@morningstar:~/Downloads/PicoCTF26/challenge$ git config user.email "root@picoctf"
ghost@morningstar:~/Downloads/PicoCTF26/challenge$ git config user.name
git config user.email
root
root@picoctf
ghost@morningstar:~/Downloads/PicoCTF26/challenge$ echo "flag please" > flag.txt
ghost@morningstar:~/Downloads/PicoCTF26/challenge$ git add -f flag.txt
ghost@morningstar:~/Downloads/PicoCTF26/challenge$ git commit -m "Add flag"
[master 20b3924] Add flag
 1 file changed, 1 insertion(+)
 create mode 100644 flag.txt
ghost@morningstar:~/Downloads/PicoCTF26/challenge$ git push origin master

```

```
picoCTF{1mp3rs0n4t4_g17_345y_506743df}
```

---
