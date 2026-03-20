# DISKO 4 — 200 pts

**Category:** Forensics  
**Author:** Darkraicg492

## Overview

Another disk image challenge. This time they straight up tell you the file was deleted and dare you to recover it.

## Approach

Decompressed the image:

```bash
gunzip disko-4.dd.gz
```

Ran `foremost` on it. Foremost is a file carving tool that scans raw disk data looking for file signatures regardless of whether the filesystem says the file exists:

```bash
foremost -i disko-4.dd -o ~/recovered
```

Also ran a quick strings and grep directly on the image:

```bash
strings disko-4.dd | grep "picoCTF{"
```

Flag showed up. Deleting a file doesnt erase the data, it just marks the space as available. Until something overwrites those sectors the original data is still right there.
