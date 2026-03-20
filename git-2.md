# Git 2 — 400 pts

**Category:** Forensics  
**Author:** LT 'syreal' Jones

## Overview

You get a compressed disk image. The story is that agents interrupted someones disk deletion routine and you need to recover a git repo from it. The hint says the deletion was interrupted before any git objects were touched.

## Approach

Decompressed and took a look at what we're working with:

```bash
gunzip disk.img.gz
file disk.img
fdisk -l disk.img
```

Mounted the image to browse the filesystem:

```bash
mkdir /mnt/disk
sudo mount -o loop disk.img /mnt/disk
```

Found a `.git` directory sitting in there. Since the hint told us git objects were untouched the full commit history should still be intact. Dug through the log:

```bash
cd /mnt/disk
git log --all --oneline
```

Checked out different commits and branches:

```bash
git show <commit-hash>
```

The flag was in a previous commit. Whoever tried to delete it forgot that git keeps a record of everything.

## Why this matters

This happens in real life constantly. People commit API keys or passwords by accident, delete them in the next commit, and think the problem is solved. It isnt. Anything thats ever been committed lives in the git history until you do something like `git filter-branch` or use BFG Repo Cleaner to actually rewrite history. Just deleting and recommitting does nothing.
