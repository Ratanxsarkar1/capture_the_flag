![](../attachments/Cryptography-8.png)

``` python
from pwn import xor

# The knowns from your output
c1 = "d7481d89f1aaf5a857f56edd2ae8994c"
c2 = "8c7d66558130eb5796d131beb43c9934"
pt1_hex = "72616e646f6d64617461313131313131" # "randomdata111111"

def to_matrix(hex_string):
    bytes_list = [int(hex_string[i:i+2], 16) for i in range(0, 32, 2)]
    array = [[0] * 4 for _ in range(4)]
    for i in range(16):
        row = i % 4
        col = i // 4
        array[row][col] = hex(bytes_list[i])[2:].zfill(2)
    return array

def from_matrix(matrix):
    reconstructed = ""
    for col in range(4):
        for row in range(4):
            reconstructed += matrix[row][col].zfill(2)
    return reconstructed

def inv_shift_rows(state):
    # Inverts the specific shifts from the vulnerable implementation
    state[1][0], state[1][1], state[1][2], state[1][3] = state[1][3], state[1][0], state[1][1], state[1][2]
    state[2][0], state[2][1], state[2][2], state[2][3] = state[2][2], state[2][3], state[2][0], state[2][1]
    state[3][0], state[3][1], state[3][2], state[3][3] = state[3][1], state[3][2], state[3][3], state[3][0]
    return state

def gmul(a, b):
    b = int(b, 16)
    p = 0
    for c in range(8):
        if b & 1:
            p ^= a
        a <<= 1
        if a & 0x100:
            a ^= 0x11b
        b >>= 1
    return p

def inv_mix_columns(s):
    # Standard AES Inverse MixColumns multipliers: 0x0e, 0x0b, 0x0d, 0x09
    ss = [[0] * 4 for _ in range(4)]
    for c in range(4):
        ss[0][c] = hex(gmul(0x0e, s[0][c]) ^ gmul(0x0b, s[1][c]) ^ gmul(0x0d, s[2][c]) ^ gmul(0x09, s[3][c]))[2:].zfill(2)
        ss[1][c] = hex(gmul(0x09, s[0][c]) ^ gmul(0x0e, s[1][c]) ^ gmul(0x0b, s[2][c]) ^ gmul(0x0d, s[3][c]))[2:].zfill(2)
        ss[2][c] = hex(gmul(0x0d, s[0][c]) ^ gmul(0x09, s[1][c]) ^ gmul(0x0e, s[2][c]) ^ gmul(0x0b, s[3][c]))[2:].zfill(2)
        ss[3][c] = hex(gmul(0x0b, s[0][c]) ^ gmul(0x0d, s[1][c]) ^ gmul(0x09, s[2][c]) ^ gmul(0x0e, s[3][c]))[2:].zfill(2)
    
    for i in range(4):
        for j in range(4):
            s[i][j] = ss[i][j]
    return s

# 1. XOR the two ciphertexts to cancel out the key entirely
delta_c = xor(bytes.fromhex(c1), bytes.fromhex(c2)).hex()

# 2. Run the difference backwards through the linear operations (L^-1)
state = to_matrix(delta_c)

# Reverse round 10 (just shift_rows)
inv_shift_rows(state)

# Reverse rounds 9 to 1 (mix_columns then shift_rows)
for _ in range(9):
    inv_mix_columns(state)
    inv_shift_rows(state)

delta_p = from_matrix(state)

# 3. XOR the resulting plaintext difference with the known plaintext to get the flag
flag_bytes = xor(bytes.fromhex(delta_p), bytes.fromhex(pt1_hex))

print(f"Recovered Flag: {flag_bytes.decode('utf-8', errors='ignore')}")
```

```
picoCTF{spi1cy!}
```

---
