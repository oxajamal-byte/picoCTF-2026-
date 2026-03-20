# offset-cycleV2

**Category:** Binary Exploitation

## Overview

The challenge generates a C program with a buffer overflow and a canary check. Theres a `win()` function that prints the flag but you need to hijack execution to reach it. The canary is the first 4 bytes of `flag.txt` which in picoCTF is always "pico".

## Approach

First I checked the generated C source to find the buffer size. Then I used GDB to look at the stack layout and figure out how much padding I needed between my input and the return address:

```bash
gdb -batch -ex "disas vuln" ./binary
```

The `sub $0xf4,%esp` instruction told me the stack frame size. From there I worked out the offset to the canary and then to the return address.

Since the canary is just the first 4 bytes of the flag file I knew it would be `pico` in ASCII. The plan:

1. Fill the buffer with junk
2. Place `pico` at the canary offset so the check passes
3. Overwrite the return address with `win()`

Built the payload with pwntools:

```python
from pwn import *

win_addr = 0x08049316
canary = b"pico"

payload = b"A" * BUFSIZE + canary + p32(win_addr) * 10
```

Sprayed the address a few times at the end because the exact offset can vary with alignment. Sent it to the remote server and got the flag.

Honestly GDB carried me on this one. Without being able to disassemble and look at the stack layout I would have been guessing offsets for hours. Buffer overflows are conceptually simple but getting the exact byte counts right is where all the actual work is.
