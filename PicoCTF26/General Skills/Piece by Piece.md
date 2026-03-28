
![](attachments/General%20Skills-8.png)

```
ssh ctf-player@dolphin-cove.picoctf.net -p 55936
```


![](attachments/General%20Skills-9.png)

```
- The flag is split into multiple parts as a zipped file.
- Use Linux commands to combine the parts into one file.
- The zip file is password protected. Use this "supersecret" password to extract the zip file.
- After unzipping, check the extracted text file for the flag.

```

```
cat part_* > flag.zip
ctf-player@pico-chall$ ls
flag.zip  instructions.txt  part_aa  part_ab  part_ac  part_ad	part_ae
ctf-player@pico-chall$ unzip flag.zip
Archive:  flag.zip
[flag.zip] flag.txt password: 
 extracting: flag.txt                
ctf-player@pico-chall$ ls
flag.txt  flag.zip  instructions.txt  part_aa  part_ab	part_ac  part_ad  part_ae
ctf-player@pico-chall$ cat flag.txt 
```

```
picoCTF{z1p_and_spl1t_f1l3s_4r3_fun_574adc66}
```

---
