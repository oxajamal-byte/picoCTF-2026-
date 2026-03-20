# picoCTF 2026 Writeups

My first CTF ever. Competed solo in picoCTF 2026, the world's largest cybersecurity competition organized by Carnegie Mellon University. The competition ran from March 7 to 17 with over 90,000 teams globally and 14,000 in the US division. Teams can have up to five members. I competed alone.

**Results:**
- Top 100 out of 14,000+ teams in the US
- 530 out of 90,000+ teams globally
- Solved around 65 challenges across all six categories

---

## Writeups

**General Skills**

- [Undo](general-skills/undo.md) — 100 pts

**Forensics**

- [Git 2](forensics/git-2.md) — 400 pts
- [DISKO 4](forensics/disko-4.md) — 200 pts

**Cryptography**

- [Not TRUe](cryptography/not-true.md) — 400 pts
- [Secure Dot Product](cryptography/secure-dot-product.md) — 300 pts

**Web Exploitation**

- [Secret Box](web-exploitation/secret-box.md) — 200 pts

**Binary Exploitation**

- [offset-cycleV2](binary-exploitation/offset-cycle-v2.md) — 400 pts
- [Heap Overflow](binary-exploitation/heap-overflow.md) — 300 pts

**Blockchain**

- [VulnBank](blockchain/vulnbank.md) — 400 pts
- [AccessControl](blockchain/access-control.md) — 200 pts
- [IntOverflowBank](blockchain/int-overflow.md) — 300 pts

---

## Tools I Used

Throughout the competition I mostly worked in Kali Linux and used tools like GDB, Ghidra, pwntools, Burp Suite, Wireshark, foremost, sleuthkit, CyberChef, and a lot of custom Python scripts. For the blockchain challenges I ended up doing everything through raw JSON-RPC calls because the competition environment had no disk space for installing libraries, which honestly taught me more than using web3.py would have.

## About picoCTF

[picoCTF](https://picoctf.org) is a free cybersecurity competition created by Carnegie Mellon University's CyLab. Challenges cover cryptography, web exploitation, reverse engineering, binary exploitation, forensics, and general skills. It runs every year and is open to everyone.
