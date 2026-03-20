# Secure Dot Product — 300 pts

**Category:** Cryptography  
**Author:** watermelon, Donkey

## Overview

A server computes dot products between your input vector and a secret AES key vector. It only accepts vectors that pass a trust verification check. The flag is encrypted with AES and you need to extract the key through the dot product service to decrypt it.

## Approach

I started by reading the source code carefully. The server has a list of trusted vectors and verifies trust by hashing the string representation of each vector. The input parsing function sanitizes your input by stripping everything except digits, commas, and brackets.

The vulnerability is in the gap between how the hash function sees your input and how the parser sees it. The hash is computed on the raw string you send. The parser strips out extra characters before evaluating. So you can craft an input that hashes to match a trusted vector but gets parsed into something completely different.

The goal was to submit unit vectors like `[1,0,0,...,0]` because the dot product of a unit vector with the key gives you the exact key byte at that position. By extracting one byte at a time I rebuilt the entire AES key.

Once I had the full key I decrypted the AES-CBC encrypted flag using the recovered key and the IV from the challenge.

Parsing inconsistencies like this are everywhere in real software. Two different functions interpreting the same input differently is basically a recipe for security bugs. The encryption itself was fine here, the key management was the problem. Doesnt matter how strong your AES is if someone can just extract the key through a side channel.
