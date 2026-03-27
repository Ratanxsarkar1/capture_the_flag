![](../attachments/Cryptography-2.png)

```python
from Crypto.Util.number import bytes_to_long, long_to_bytes
from Crypto.Random import get_random_bytes

key = bytes_to_long(get_random_bytes(126))

def steplfsr(lfsr):
    b7 = (lfsr >> 7) & 1
    b5 = (lfsr >> 5) & 1
    b4 = (lfsr >> 4) & 1
    b3 = (lfsr >> 3) & 1

    feedback = b7 ^ b5 ^ b4 ^ b3
    lfsr = (feedback << 7) | (lfsr >> 1)
    return lfsr

def encrypt_lfsr(pt_bytes):
    output = bytearray()
    lfsr = key & 0xFF
    for p in pt_bytes:
        lfsr = steplfsr(lfsr)
        ks = lfsr
        output.append(p ^ ks)
    return bytes_to_long(bytes(output))

pt = b"[redacted]"
ct = encrypt_lfsr(pt)

print(long_to_bytes(ct).hex())
```

```
21c1b705764e4bfdafd01e0bfdbc38d5eadf92991cdd347064e37444e517d661cea9
```

```python
from Crypto.Util.number import long_to_bytes

cipher_hex = "21c1b705764e4bfdafd01e0bfdbc38d5eadf92991cdd347064e37444e517d661cea9"
ct = bytes.fromhex(cipher_hex)

def steplfsr(lfsr):
    b7 = (lfsr >> 7) & 1
    b5 = (lfsr >> 5) & 1
    b4 = (lfsr >> 4) & 1
    b3 = (lfsr >> 3) & 1
    feedback = b7 ^ b5 ^ b4 ^ b3
    return ((feedback << 7) | (lfsr >> 1)) & 0xFF

for seed in range(256):
    lfsr = seed
    pt = []

    for c in ct:
        lfsr = steplfsr(lfsr)
        ks = lfsr
        pt.append(c ^ ks)

    pt_bytes = bytes(pt)

    if b"picoCTF{" in pt_bytes:
        print("Seed:", seed)
        print(pt_bytes)
```

```
picoCTF{l1n3ar_f33dback_sh1ft_r3g}
```

---
