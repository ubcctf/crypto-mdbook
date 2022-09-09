# Cryptopals Set 3

<!-- toc -->

## Intro
   * For me, this is the set where things really started to get fun
   * This note at the start made me really hyped and I hope it makes you excited too
      * “We've also reached a point in the crypto challenges where all the challenges, with one possible exception, are valuable in breaking real-world crypto.”

## Challenge 17
   * This is a great challenge
      * CBC is (unfortunately) still a relatively popular block cipher mode, and is seen as "the good alternative" to ECB
      * This directly builds off of what you learned about CBC decryption in challenge 16, how bit flips in one ciphertext block affect the resulting decryption in the next block
      * This shows off how useful these side channel leaks are. A **side channel leak** is when a system unintentionally reveals information about it's inner workings
         * For this challenge, the "decryption server" is leaking the fact that the padding is invalid
         * For later challenges you'll see that even leaking how long the code takes to run can be enough to cryptography
         * Some other side channels you won't see in cryptopals: 
            * The amount of power the CPU is using can be used to retrieve AES keys from smart cards
            * Using information about the CPU cache to break OpenSSL's carefully implemented RSA algorithm https://web.eecs.umich.edu/~genkin/cachebleed/index.html
      * CBC padding oracles also show up from time to time in CTFs, though more rarely due to how famous this attack is
   * Here is a good explanation of the attack: https://robertheaton.com/2013/07/29/padding-oracle-attack/ 
   * From my experience this challenge is not necessarily conceptually difficult, but can be a bit tricky to get right
      * Start with just finding one byte, then work towards automating it for the rest of the bytes in the block, and then finally for multiple blocks
      * Made sure the padding functions from set 2 are fully correct
         * A plaintext that is all padding should be accepted
         * A plaintext with no padding should be rejected
   * Aside: Anyone else feeling that dread after realizing that all it takes to break a perfectly secure algorithm like AES and a reasonably sensible mode like CBC is something as small as having two different error messages for wrong password vs bad padding? Because I definitely was