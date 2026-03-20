# Undo — 100 pts

**Category:** General Skills  
**Author:** Yahaya Meddy

## Overview

The challenge drops you into a server and asks you to reverse some Linux text transformations. The only hint is to look into the `tr` command.

## Approach

Connected to the server with netcat and saved the output to a file so I could mess with it without reconnecting every time:

```bash
nc foggy-cliff.picoctf.net 62188 | tee output.txt
```

The output was garbled text. Clearly some kind of character substitution. Since the hint pointed directly at `tr`, I tried ROT13 first. ROT13 shifts every letter 13 positions in the alphabet and applying it twice gives you the original back:

```bash
cat output.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

Flag came right out. Easy 100 points and a good warmup for the rest of the competition. Got into the habit of saving server output to a file before doing anything with it which saved me a lot of reconnecting on later challenges.
