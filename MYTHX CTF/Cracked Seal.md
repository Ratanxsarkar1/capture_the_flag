## **Challenge Overview**

**Name:** Cracked Seal
**Category:** Web  
**Difficulty:** Medium
**Points**: 200


###### Challenge Description

An internal admin portal guards its gates with signed tokens.  
 Every visitor gets a pass — but only the right kind opens the inner door.

 The seal that binds these tokens was chosen in haste.  
 A warrior with the right wordlist might break it in seconds.

 Forge your way in.
 
---

Login in the given Portal as Guest:

![](attachments/Untitled-37.png)

**Token Found:**

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoiZ3Vlc3QiLCJyb2xlIjoiZ3Vlc3QiLCJleHAiOjE3NzQ3OTc3NjZ9.3LSN75E5larJuGnvXerM8lBzp5OdDk6jstiAU2gzAX4
```

Brute-Force the secret key of this Jwt Token using JWT_Tool
![](attachments/Untitled-38.png)

```
[+] ilovecats is the CORRECT key!
```

`Modify the Token With the secret Key and replace in the browser:`

![](attachments/Untitled-39.png)

#### After Refreshing the browser Get the flag:
![](attachments/Untitled-40.png)

**Flag:**
```
ctf7{jw7_w34k_s3cr37_cr4ck3d}
```

---
