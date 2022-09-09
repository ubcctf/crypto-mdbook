# Cryptopals Set 1

<!-- toc -->

### Intro
   * A lot of this set comes down to how comfortable you are writing code in python
   * There is a little hitch in that byte representations in python changed a lot between python2 and python3, meaning stackoverflow answers and such will be outdated and might not work

### Challenge 1: Some useful functions and notes about python bytes
   * `int(x, 16)` will parse the string x as a hex string, and return a number
   * The `Crypto.Util.number.long_to_bytes` and `Crypto.Util.number.bytes_to_long` functions from pycryptodome convert between numbers and bytes
   * Bytes in python are really just an array of ints between 0 and 255
      * `b”hi”` is really just `[104, 105]`
      * the `bytes()` constructor takes an int array and returns a bytes object
      * using a for loop or a list comprehension like `[x for x in my_bytes]` will return the int array
      * you can also index into bytes objects to get the integers, `b”hi”[0] == 104`
      * Remember that bytes are just numbers with base 255
   * `ord()` takes a single character and returns its integer value
   * `chr()` does the opposite, integer to char
   * the `base64` package has functions to go from bytes <-> base64 strings, namely `b64decode` and `b64encode`

### Challenge 2: XOR in python
   * The xor operator in python is `^` and it takes two integers and returns the result of xor
   * A note about XOR in case you aren’t familiar: The operation cancels out with itself if you do it twice
      * Ie: `A xor B xor B == A`
      * If you aren’t sure why this is the case, try writing out the table for XOR
      * This is why “encryption” and “decryption” are actually the same action when using XOR, you end up doing the exact same thing
   * How do we use `^` with bytes objects? Remember that we can index into bytes objects to get the underlying integers, so try a for loop and then combining the results afterwards with `bytes()` back into a bytes object

### Challenge 3
   * This general idea comes up sometimes in cryptography attacks, but the idea is that we know the original must have been some english sentence, so we can bruteforce and see which one is most like an english sentence
      * This idea also can be generalized to cases where we know some "structure" that the original message must be in and use that information to inform our bruteforce
   * Note: Do not be lazy and do it by eye, the “scoring” function will be needed in the next challenge
   * The `sorted()` function will probably come in handy
   * [https://en.wikipedia.org/wiki/Letter_frequency](https://en.wikipedia.org/wiki/Letter_frequency)

### Challenge 4
   * Basically the same as challenge 3 but at a larger scale, same principle applies
   * We can assume that anything that isn’t encrypted with a single character XOR will result in a garbled mess when we perform an XOR on it

### Challenge 5
   * Just coding, good luck!
   * The modulo operator `%` will probably come in handy here

### Challenge 6
   * Hamming distance function tips
      * To format an integer as a binary string, use `“{0:b}”.format(x)`
      * Use in combination with `bytes_to_long` to convert the bytes to the bit string
      * If the lengths differ, the difference in length should be added to the distance
   * Solve tips
      * Try to reuse as much code from earlier challenges as possible
      * Transposing means taking `[[a,b,c], [1,2,3]]` and making it into `[[a,1], [b,2], [c,3]]`
   * An aside
      * I’ve actually used my code for this challenge quite a few times. You might be wondering what real world algorithm uses a repeating key xor and the answer is none, but many ciphers do actually use XORs. This challenge may seem like a toy challenge, but when we get to challenge 20 in set 3, you’ll see how this attack actually works **very well** on a popular block cipher mode.

Some definitions
* **AES** (Advanced Encryption Standard) is a **block cipher**, it takes a block of 16 bytes and garbles it based on a 16 byte key
   * However this presents a problem, what do you do if your message is longer than 16 bytes, for example a 32 byte message?
   * If you’re curious about what AES does under the hood (not needed for these challenges, but fun to learn about) https://www.youtube.com/watch?v=O4xNJsjtN6E
* **ECB** stands for Electronic Code Book, and is a **block cipher mode of operation**. Block cipher modes are ways of making block ciphers (which can only encrypt a single block) usable for larger messages
   * ECB is the most straightforward, cut the message into blocks and encrypt each of them separately.
   * This turns out to be a terrible way of doing things, and you’ll see why in the next few challenges
   * https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Electronic_codebook_(ECB)
  
### Challenge 7

   * pycryptodome provides an AES implementation in Crypto.Cipher.AES
      * https://pycryptodome.readthedocs.io/en/latest/src/cipher/aes.html
   * You should make both encryption and decryption functions, you’ll need it in a bit
  
### Challenge 8
   * There is a hidden assumption in this challenge that I think really should have been mentioned. **The challenge assumes that the plaintext must have a repeated block**. 
   * The important point here is that ECB is the only cipher mode that has this property, that the same plaintext blocks will result in the same ciphertext blocks
      * This weakness of ECB turns out to cause many many problems, which you’ll see in set 2
      * The worst part is ECB is seen as the “default” setting for block ciphers, despite it being almost always a terrible idea