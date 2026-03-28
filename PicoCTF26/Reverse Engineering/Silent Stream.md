![](attachments/Reverse%20Engineering-2.png)

We are given:
- A **PCAP file** containing network traffic.
- A **Python encoding script** used by the sender.

The challenge asks us to **reconstruct the original file transferred over the network**.
 Initial Analysis
 
The provided encoding script is:

```python
import socket

def encode_byte(b, key):
    return (b + key) % 256

def simulate_flag_transfer(filename, key=42):
    print(f"[!] flag transfer for '{filename}' using encoding key = {key}")

    with open(filename, "rb") as f:
        data = f.read()

    print(f"[+] Encoding and sending {len(data)} bytes...")

    for b in data:
        encoded = encode_byte(b, key)
        pass

    print("Transfer complete")

if __name__ == "__main__":
    simulate_flag_transfer("flag.txt")
```

### Observations

The encoding function performs a simple byte-wise transformation:

```
encoded_byte = (original_byte + key) % 256
```

The key used is:

```
key = 42
```

To recover the original data we simply reverse the operation:

```
original_byte = (encoded_byte - 42) % 256
```

This indicates that the **transmitted file inside the PCAP is encoded using a simple additive cipher**.

## Extracting the Encoded Data from the PCAP

The PCAP contains full packet structures (Ethernet, IP, TCP headers), so we must extract **only the TCP payload**.

Using **tshark**:

```bash
tshark -r packets.pcap -T fields -e tcp.payload | tr -d '\n' | xxd -r -p > encoded.bin
```

Explanation:

| Command           | Purpose                        |
| ----------------- | ------------------------------ |
| `-r packets.pcap` | Reads the PCAP file            |
| `-e tcp.payload`  | Extracts only TCP payload data |
| `tr -d '\n'`      | Removes line breaks            |
| `xxd -r -p`       | Converts hex to raw binary     |

This produces a binary file:
```
encoded.bin
```

### Decoding the Transferred File

Next we reverse the encoding.
```python
key = 42

with open("encoded.bin", "rb") as f:
    data = f.read()

decoded = bytes((b - key) % 256 for b in data)

with open("decoded_file", "wb") as f:
    f.write(decoded)

print("Recovered file saved.")
```

This script subtracts **42 from each byte** to restore the original content.
### Identifying the File Type

We now check the file type:
```bash
file decoded_file
```

Output:
```
JPEG image data, JFIF standard
```

This confirms the recovered file is a **JPEG image**.

Running `strings` also reveals the JPEG header:
```
JFIF
```

### Inspecting the Image

Opening the image:

![](attachments/Reverse-7.png)

```flag
picoCTF{tr4ck_th3_tr4ff1c_c41f36a9}
```

---
