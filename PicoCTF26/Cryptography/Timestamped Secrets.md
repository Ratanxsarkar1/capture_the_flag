![](../attachments/Cryptography-10.png)

```python
from hashlib import sha256
import time
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad

def encrypt(plaintext: str, timestamp: int) -> str:
    timestamp = int(time.time())
    key = sha256(str(timestamp).encode()).digest()[:16]
    cipher = AES.new(key, AES.MODE_ECB)
    padded = pad(plaintext.encode(), AES.block_size)
    ciphertext = cipher.encrypt(padded)
    return ciphertext.hex()

if __name__ == "__main__":
  
    plaintext = "picoCTF{...}"
    result = encrypt(plaintext, key)
    print(f"Hint: The encryption was done around {timestamp} UTC\n")
    print(f"Ciphertext (hex): {ciphertext.hex()}\n")
```

```result
Hint: The encryption was done around 1770242601 UTC
Ciphertext (hex): 2849cce932845f9864c369cf519473dd9b54ce1105c02305886bdc8690134711
```

```python
from hashlib import sha256
from Crypto.Cipher import AES
from Crypto.Util.Padding import unpad

cipher_hex = "2849cce932845f9864c369cf519473dd9b54ce1105c02305886bdc8690134711"
cipher = bytes.fromhex(cipher_hex)

approx_time = 1770242601

for t in range(approx_time - 200000, approx_time + 200000):

    key = sha256(str(t).encode()).digest()[:16]

    cipher_obj = AES.new(key, AES.MODE_ECB)

    try:
        pt = unpad(cipher_obj.decrypt(cipher), 16)

        if b"picoCTF" in pt:
            print("FOUND!")
            print("timestamp:", t)
            print("flag:", pt.decode())
            break

    except:
        pass
```


```
picoCTF{sa3S_sEc9t_16d80a85}
```

---
