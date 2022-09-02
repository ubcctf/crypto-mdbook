# One two three

## Challenge

Ok so ECB mode was a bust, what else can we try? What if don't use blocks at all?

- [encryptor.py](/challenge-sources/one_two_three/encryptor.py)
- [secret.enc](/challenge-sources/one_two_three/secret.enc)

## Guide
Good job figuring out the last challenge!

You saw that ECB mode has one crucial weakness, each block gets encrypted and decrypted exactly the same way, no matter where it's located in the ciphertext. This led you to be able to move blocks around to wherever you wanted and have the plaintext change in the same way.

So now that we know ECB is bad, how can we circumvent this problem? How can we make our cipher mode not have this problem?

Primer: The one time pad 
---
Let's say I want to encrypt a one byte message, and I decide to do so by XORing it with a random byte. I then happily send this off and you happen to be able to intercept it.

So you have this one byte encrypted message, which you know is something that I encrypted via XOR. Is it possible for you to figure out what the original message was?

It turns out that the answer is no! If the byte I used for the XOR was random, then the resulting encrypted byte is also completely random and unrelated in any way to my original message.

This is what is called "information theoretically secure". Even if you had infinite time, you could never figure out which message my original byte was. This encryption scheme is called the [One-time pad](https://en.wikipedia.org/wiki/One-time_pad)

Now back to AES

## Counter mode

Let's say we want to bring that idea to reality, how can we generate a bunch of random bytes to xor our message against? 

This stream of random bytes needs to be
- Able to be generated from the key, so we can regenerate it when we want to decrypt the message
- But still random enough that it's secure

Here's how Counter (CTR) mode achieves this
1. Start a counter at c = 1
2. Pad c out to 16 bytes and encrypt it with your AES key
3. Then you have 16 random bytes, use that to XOR with your message
4. Then increment the counter and continue until you have enough random bytes to encrypt your entire message

So the resulting ciphertext is like
- The first 16 bytes are the first 16 bytes of the plaintext XORd with the aes encryption E of the byte 1, E(pad(1))
- The next 16 bytes are plaintext_2 XOR E(pad(2))
- then plaintext_3 XOR E(pad(3)) and so on

The stream of random bytes, ie E(pad(1)) | E(pad(2)) | E(pad(3)) ... is called the keystream

This evidently solves the issue with ECB we saw earlier, because if you move a block around then it'll be something completely different when you decrypt it, since it was encrypted with a different part of the keystream.

## The twist

Actually I lied, the description I gave is not the real CTR mode, because it has a crucial weakness!

Your job is to find this weakness and decrypt the messages found in `secret.enc`

To solve this you'll need to figure out what this weakness is, use some googling to figure out why this weakness is so critical, and learn how you can exploit it.

Some tips:
- `secret.txt` contains many lines of english text and, of course, the flag
- You may find that your code from the first challenge, "Copilot my savior", will come in handy
- There's no shame in buying hints if you're stuck!

## Aside

As is the pattern with the earlier challenges, this is actually a mistake that you can make when using CTR mode. Here's an excerpt from a paper about a very closely related cipher mode, GCM mode.

"We investigate (redacted) issues with the GCM block cipher mode as used in TLS and focus in particular on AES-GCM, the most widely deployed variant. With an Internet-wide scan we identifed 184 HTTPS servers (redacted), which fully breaks the authenticity of the connections. Affected servers include large corporations, financial institutions, and a credit card company"

## Hints

If you really need some hints, I've left some base64 encoded here
1. `TG9vayBjYXJlZnVsbHkgYXQgdGhlIGVuY3J5cHQgZnVuY3Rpb24uIEl0IGdlbmVyYXRlcyB0aGUga2V5c3RyZWFtIGZ1bGx5IGluZGVwZW5kZW50bHkgb2YgdGhlIHBsYWludGV4dCEgVGhpcyBtZWFucyB0aGF0IHRoZSBrZXlzdHJlYW0gaXMgaWRlbnRpY2FsIGZvciBlYWNoIHBsYWludGV4dC4gS25vd2luZyB0aGlzLCB3aGF0IGNhbiB5b3UgZG8/Cg==`
2. `V2Uga25vdyB0aGF0IHRoZSBrZXlzdHJlYW0gaXMgdGhlIHNhbWUgZm9yIGVhY2ggcGxhaW50ZXh0LCBidXQgd2hhdCBkb2VzIHRoaXMgbWVhbj8gVGhpcyBtZWFucyB0aGF0IHRoZSBmaXJzdCBieXRlIG9mIGVhY2ggbGluZSBpcyBYT1JkIGFnYWluc3QgdGhlIHNhbWUgYnl0ZSwgaWUgdGhlIGZpcnN0IGJ5dGUgb2YgdGhlIGtleXN0cmVhbS4gU2FtZSBmb3IgdGhlIHNlY29uZCBieXRlIG9mIGVhY2ggbGluZSBhbmQgc28gb24uIFRoaXMgaXMgcmVhbCBzaW1pbGFyIHRvIHRoZSBjb3BpbG90IGNoYWxsZW5nZSBpc24ndCBpdCEgWW91IGNhbiBndWVzcyBieXRlcyBpbiB0aGUgc2FtZSB3YXksIGJ1dCB5b3UgbmVlZCB0byBiZSBzbWFydGVyIGFib3V0IGZpZ3VyaW5nIG91dCB3aGVuIGEgZ3Vlc3MgaXMgJ2NvcnJlY3QnCg==`
3. `SG93IGNhbiB3ZSB0ZWxsIHdoZW4gYSBndWVzcyBpcyBjb3JyZWN0PyBXZWxsIHdlIGtub3cgdGhhdCB0aGUgdGV4dCBpcyBlbmdsaXNoLiBTbyBjYW4gYXNzaWduIGVhY2ggZ3Vlc3MgYSAnc2NvcmUnIGJhc2VkIG9uIGhvdyAnZW5nbGlzaCcgdGhlIHJlc3VsdCBpcy4gRm9yIGV4YW1wbGUsIGFkZGluZyBwb2ludHMgZm9yIGxldHRlcnMsIG51bWJlcnMsIHB1bmN0dWF0aW9uLCBhbmQgd2hpdGVzcGFjZSwgd2hpbGUgc3VidHJhY3RpbmcgcG9pbnRzIGZvciBlYWNoIGJ5dGUgdGhhdCBkb2Vzbid0IGZpdC4K`