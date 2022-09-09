# Cryptopals Set 2

<!-- toc -->

### Challenge 9
   * Fairly straightforward, just some more programming


### Challenge 10: A new block cipher mode, CBC
   * **CBC** or Cipher block chaining is another block cipher mode
      * The goal of CBC is to not be deterministic like ECB, ie two identical plaintext blocks should encrypt to _different_ ciphertext blocks
      * How does it accomplish this?
         * CBC requires an extra **initialization vector** or IV for short, which is just random bytes the size of a block
         * For each plaintext block we want to xor our plaintext with something first, and then encrypt it with our cipher
            * For the first block we xor it with the IV before encrypting
            * For every other block we xor it with the _last ciphertext block_
         * Essentially “chaining” the different blocks together, so the resulting ciphertext of a block depends on the “sum” of all the previous blocks and the IV
      * https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher_block_chaining_(CBC) has some very useful diagrams
   * Implementing it is fairly straightforward once you understand whats going on
   * Decryption is just running this in reverse, block cipher decryption first and then xor
   * Note: ECB mode with one block is the same as just running the cipher, so you can reuse that as long as you’re encrypting/decrypting only one block
  
![CBCEncryption](/assets/images/cbc_encryption.png)
  
### Challenge 11
   * This is a bit of a weird challenge, I’m not really sure what it’s accomplishing?
   * I don’t think there’s a good way to detect CBC mode, so I just detected ECB mode and then guessed CBC otherwise
   * Again, it only works if you send a plaintext with repeated blocks
   * Idk, maybe skip this one, it kinda comes back in challenge 12 but as an “optional” thing

### Challenge 12
   * Now don’t skip this one though, because it’s really cool (and also shows up in real CTFs!)
   * The explanation is pretty good for how to get the first byte of the unknown-string, but the next step and automating it can be a bit tricky
      * For the next byte you would first send 14 A’s + the first byte of the unknown string
         * The first block would then be aes(“A”s + first byte + second byte)
      * Then you want to start sending 13 A’s + first byte + guesses for the second byte
      * And then like last time stop when you find a match
   * The congratulations at the bottom is pretty accurate for CTFs too, every once in awhile I see another one of these pop up
      * [Here’s the last one I remember](https://ctftime.org/writeup/18675)

### Challenge 13: Cut and paste
   * This one is fun to figure out, it’s the first time the authors really let you out and try to figure out how to do what it wants
   * The title is a big hint, if we could copy paste things, what _would_ we want to cut and replace?
   * Given that this is ECB mode, what exactly can we cut and replace? (bits? bytes? characters? blocks? messages?)

### Challenge 14
   * Some clarification on this challenge, I originally thought the random prefix would be generated each time, a new random prefix of random length each time you touch the oracle
   * I honestly don’t really know how one would go about solving that, so I and everyone else who has write ups for cryptopals instead assumed that the random prefix would be generated once and be reused for all later oracle calls
   * So now the trouble is really just one thing, how long is that random prefix? How can you figure that out?

### Challenge 15
   * More programming stuff, this is just setup for challenge 17, which is gonna be a big one

### Challenge 16
   * Another fun one to figure out
   * Try to think about what happens in CBC decryption with the user data block and the block after it
   * How can we completely replace the second ciphertext block in a way to make the third block decrypt to what we want, namely “;admin=true;”? What happens to the second plaintext block in that case?