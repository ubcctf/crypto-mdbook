## Cryptopals companion

# THIS IS A WORK IN PROGRESS! THE FORMATTING WILL BE LESS GARBAGE AFTER IM DONE WITH IT

## Preparations before we start
* This companion in general will not provide any direct solutions, I instead mostly give leading questions. If you need solutions, plenty of solutions and writeups are just a google away, though remember that looking at the answers at the back of the book leads to understanding less. Feel free to DM me on discord or in the `crypto` channel if you're stuck
* Almost all ctfers use python for solving challenges across basically all categories, so that’s what I would recommend
   * For python, all you’ll need is
      * A working python installation
      * [pycryptodome](https://pypi.org/project/pycryptodome/)
      * Something to write code with, `vscode` is nice
   * I’ll be assuming you’ll be writing in python for this guide
* Make sure you read the homepage, everything it says is true
   * You don’t need (and aren’t expected to) know any cryptography beforehand
      * They do unfortunately skip out on defining some terms, but that’s what this companion is for
   * You only need simple math 
      * The hard math is left to the professionals and we just copy their equations :)
      * No math shows up until set 5 anyway 
   * These challenges are attacks, not puzzles with tricks. The challenge authors make an effort to make the challenges clear and "doable", instead of obfuscated like you'd see in competitions. This companion guide also helps clear up the occasional ambiguity and confusing wording
   * I like to put an extra little disclaimer whenever I recommend someone take a look at cryptopals, which is that after solving these challenges most people feel a strong feeling of dread. Dread when they realize how fragile cryptography can be and how most people writing code that uses cryptography are **completely unaware** that these fragile points exist
* The general structure of the sets is
   * Set 1 is preparation and “the qualifier set” 
   * Sets 2-4 are various attacks on symmetric ciphers and a few hashes in set 4
   * Sets 5-6 are attacks on various asymmetric primitives, all using primes and numbers
* In case you’re wondering how well cryptopals will prepare you for CTFs, take a look at CSAW CTF 2020. Three challenges are basically directly taken from cryptopals and can be solved by copying over the code
   * Authy is a length extension sha attack, covered in challenge 29
   * modus operandi is a ciphertext detection challenge, covered in challenge 11
   * adversarial is a fixed nonce CTR, covered in challenges 6 and 20

Some quick definitions
---
**Encryption**
   * Encryption is turning a message (like “cryptography is cool”) and changing into a message that appears to be a garbled mess (like “falkjdior30vjs”) based on some “key”
   * The method of encrypting the message and what the key is vastly depends on the algorithm, for example in rsa the key is a number, in caesar ciphers the key is a table, and in aes the key is 16 bytes
   * **Plaintext** is used to refer to the message before encryption and **ciphertext** is used for the garbled message after encryption