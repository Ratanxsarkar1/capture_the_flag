![](attachments/General%20Skills-16.png)

```
import sys

while(True):
  try:
    print('⊹──────[ BYTEMANCY-2 ]──────⊹')
    print("☍⟐☉⟊☽☈⟁⧋⟡☍⟐☉⟊☽☈⟁⧋⟡☍⟐☉⟊☽☈⟁⧋⟡☍⟐")
    print()
    print('Send me the HEX BYTE 0xFF 3 times, side-by-side, no space.')
    print()
    print("☍⟐☉⟊☽☈⟁⧋⟡☍⟐☉⟊☽☈⟁⧋⟡☍⟐☉⟊☽☈⟁⧋⟡☍⟐")
    print('⊹─────────────⟡─────────────⊹')
    print('==> ', end='', flush=True)
    user_input = sys.stdin.buffer.readline().rstrip(b"\n")
    if user_input == b"\xff\xff\xff":
      print(open("./flag.txt", "r").read())
      break
    else:
      print("That wasn't it. I got: " + str(user_input))
      print()
      print()
      print()
  except Exception as e:
    print(e)
    break
```

script.py

```
from pwn import *

host = "lonely-island.picoctf.net"
port = 64132

p = remote(host, port)

p.recvuntil(b'==> ')

p.sendline(b"\xff\xff\xff")   # IMPORTANT

print(p.recvall().decode())
```

![](attachments/General%20Skills-17.png)

```
picoCTF{3ff5_4_d4yz_c689238e}
```
