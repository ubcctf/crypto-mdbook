# Frequently asked questions

<!-- toc -->

## Why cryptography?

It's a lot of fun! It feels great to think something is impossible to break, spend hours starting at it, and then eventually pry it apart and break it into pieces to make it decrypt out your flag.

The way I like to think about it is that solving CTF challenges usually involves trying to do something under a set of constraints. In binary exploitation the constraints are things like the state of the program, the stack, and the heap. In web the constraints are the various protections that websites implement.

In cryptography the constraints that we have to figure out how to weave our way through are the protocols themselves, the mathematics behind the operations and/or the implementation of them in the real world. I find crypto a lot of fun because these rules are arbitrary, they're just whatever the challenge author or protocol author thought of, leading to each challenge having it's own unique flavor rather than always having to deal with things like ASLR.

Cryptography is also uniquely vast in the kinds of ways that people try (and fail) to make connections secure, and the ways that we find to attack these protocols are also uniquely diverse. Having so many different ideas underpinning cryptography means there's a lot of things to learn and it's likely you'll find something that clicks for you and something you'll enjoy attacking, whether that's high level math-based attacks or low level cpu side-channel based attacks.

TLDR: Crypto challenges feel fresh and new because of the freedoms challenge authors have when writing their challenges. There's also an extremely wide range of cryptographic attacks and techniques so you can really look for what you find fun

## What does attacking cryptography teach you?

Unfortunately, since not many people will ever have to write their own crypto code, cryptography as a CTF category is less useful for a typical CS career than things like pwn or web which teach you directly applicable skills for memory and website security respectively.

However this doesn't mean that cryptography doesn't teach you anything! Crypto and other CTF categories teach you one extremely important thing, which is arguably the most important thing you can learn by doing CTFs, an attacker's mindset. 

What is an "attacker's mindset"? It's a way of thinking where you pick and pry and try to break whatever bit of code you're looking at. It's a way of reading code where you carefully examine each part and consider what assumptions each function makes and how that might go wrong. It's understanding code not just for what it wants to do, but trying to prove in your head that it _only_ does what it wants to do and can't be manipulated otherwise.

Experience doing this is highly useful in security obviously, but is also just useful for writing correct code in general. Most modern programming languages don't provide many guarantees (rip dependent types) on correctness or state and it often comes down to the programmer to be able to mentally check the preconditions and postconditions of your code. If you're highly used to doing this in an attacker's mindset then you end up being quicker at finding how things can go wrong, instead of being focused on the happy paths where everything goes right

Outside of practical skills, for me a big general lesson was that _shit can go wrong really fast_. Cryptography breaks with even the smallest of mistakes and learning some crytographic attacks is a good way of really hammering that lesson in. Cryptography is extremely important but there's a reason why there's a constant stream of new algorithms and papers attacking existing ones. There's a reason why the NIST standardization process takes years to go from new algorithm to established standard.

## Is cryptography just math?

No! There's plenty to do that won't touch _any_ math at all!

Things with a lot of math:
- Most asymmetric cryptography (RSA, DH, ECC)
  - Key exchanges, signing, asymmetric encryption
- Random number generation (LCG, LFSR, MT)
- Some post quantum cryptography (Lattices)
- Quantum cryptography (Lots of physics)

Things with *no* math:
- Most symmetric cryptography (AES)
  - Ciphers, block cipher modes
  - Some attacks on cipher construction start to involve some matricies (affine, linear attacks)
- Hashing (SHA)
- Some post quantum cryptography (SPHINCS+)
- Side channel attacks (Power, timing, cache)

Disclaimer: You may find that a lot of CTFs have challenges skewed towards the math categories due to it being easier to write challenges for things like RSA and ECC. That doesn't mean that cryptography is all math, CTF stuff just tends to be skewed that way. 

## What skills do I need to get started?

Generally across the board the requirements to do easy challenges in each category is the same
- A machine set up with your programming language of choice (typically `python`) 
    - Needs to be able to do basic operations and communicate with servers (`pwnlib` for python)
- A willingness to learn
    - This is extremely important! No matter how good you get at any CTF category, you'll always be banging your head feeling like a challenge is impossible and having no idea how to solve it. Being "good" at cryptography doesn't mean you instantly know how to solve something, it means you know how to learn how to figure out to attack something.

For the general "types" of challenges you find at CTFs, there are some requirements, but these really are quite minimal. I'm not trying to make these categories seem easier than they are, they really do just don't particularly require any other CS knowledge. You really can just sit down and learn how they work.

Attacking block ciphers (AES)
- The current standard block cipher, AES, is constructed with 4 steps. Substitution, XOR, shifting rows, and shifting columns
- It turns out that some of these have mathematical representations, but at their core these operations are extremely simple. This is by design and is why AES is _so_ fast

Attacking block cipher modes (ECB, CBC, CTR, GCM)
- Block cipher modes usually involve simple operations like XORs
- GCM mode is the main exception, since it creates an authentication code with a signature as part of it's encryption. This neccessitates it being more mathematical and complicated.

Attacking hashing algorithms (SHA)
- Similarly to block ciphers, SHA2 is made up of a number of rounds that involve a number of simple steps (bit shifts and XORs only!)
    - All hashes that use the Merkle–Damgård construction are very similar (MD5)
- Common attacks usually involve a similar set of skills, lots of bit manipulations and XORS
    - Some statistical stuff maybe

Attacking RSA and Diffie Hellman
- RSA and DH rely on modular arithmetic. Understanding the basic algorithms is easy and just requires knowledge of how `mod` works
- Understanding _why_ RSA works is more involved and requires learning some number theory (Fermat's little theorem)
- Basic attacks on RSA and DH involve basic math
   - For example, all the challenges in the `cryptopals` and `beginner asymmetric` sets of challenges don't require _any_ of the more complicated math below
- More and more advanced attacks on RSA start to involve more and more complex mathematics 
   - RSA uses prime numbers and primes have a ton of unique mathematical properties that number theorists study. These sometimes become CTF challenges (eg: smooth primes)
   - Both algorithms use modular integers, or in math terms, finite Galois fields. Galois fields are extremely well studied and therefore have a lot of interesting properties that can lead to CTF challenges (eg: small subgroup confinement)
   - Neither of these are required at the start, but if you plan to really get into RSA and DH this is kinda where you're headed

Attacking ECC
- As the name implies (elliptical curve cryptography), you'll need to know about elliptical curves to learn about how ECC works
   - Elliptical curves are just a certain type of curve (like a weird sideways parabola)
   - The idea is to use points on this curve as a mathematical group because they have nice properties, so what ECC does is extend the algorithms for RSA and DH (which use Galois fields) to this new elliptical curve field. So similar algorithms, just points on a curve instead of numbers (which is weird if you haven't done this kinda math before)

[^1]: Knock on wood