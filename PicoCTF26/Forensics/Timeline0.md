![](../attachments/Forensics-2.png)

We were given a **compressed disk image** `partition4.img.gz`.  

The hint suggested:
> _Create a Sleuthkit MAC timeline! Sloppy timestomping can yield strange (very old) timestamps._

This indicates the attacker **manipulated file timestamps (timestomping)** and we must detect abnormal timestamps using forensic tools.

# Step 1 — Extract the disk image

First identify the file type:

```bash
file partition4.img.gz
```

Then decompress it:

```bash
gunzip partition4.img.gz
```

This produces:

```
partition4.img
```

# Step 2 — Identify the filesystem

Using `binwalk`:

```bash
binwalk partition4.img
```

Output showed:

```
EXT4 filesystem
```

So the image contains a **Linux EXT4 filesystem**.

# Step 3 — Generate a Sleuthkit timeline

First create a **bodyfile** using `fls`.

```bash
fls -r -m / partition4.img > bodyfile.txt
```

Then generate a **MAC timeline** using `mactime`.

```bash
mactime -b bodyfile.txt > timeline.txt
```

MAC timeline shows file activity based on:

- **M** → Modified
- **A** → Accessed
- **C** → Metadata changed
- **B** → Birth/creation

# Step 4 — Detect suspicious timestamps

Looking through the timeline revealed a strange entry:

```
Tue Jan 01 1985 ... /bin/bcab
```

This timestamp is **unusually old**, which suggests **bad timestomping**.

So the suspicious file is:

```
/bin/bcab
```

# Step 5 — Locate the inode

Using `fls`:

```bash
fls -r partition4.img | grep bcab
```

Output:

```
r/r 4945: bcab
```

So the **inode number is 4945**.

# Step 6 — Extract the file

Using `icat` from Sleuthkit:

```bash
icat partition4.img 4945 > bcab
```

Viewing the file:

```
NzFtMzExbjNfMHU3MTEzcl9oM3JfNDNhMmU3YWYK
```

# Step 7 — Decode the content

The string is **Base64 encoded**.

```bash
cat bcab | base64 -d
```

Flag:

```
picoCTF{71m311n3_0u7113r_h3r_43a2e7af}
```

---
