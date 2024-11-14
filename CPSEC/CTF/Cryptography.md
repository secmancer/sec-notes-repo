## Encoding
- Putting data in another form (usually in a way that computers can easily process)

## Binary
- Foundation of the digital world
- 1s and 0s (bits)
- Bits are often grouped into
	- Nibble: 4 bits
	- Byte: 8 bits
	- Word: (Depends on the processor)

## Binary Numbers (Decimal⇔Binary)
 - “Places” represent powers of two (instead of powers of 10 like in decimal).
 - 1: 1
 - 2: 10
 - 3: 11
 - 4: 100
 - 5: 101
 - 6: 110
 - 7: 111

## Hexadecimal (Binary⇔Text)
 - More compact way to represent binary in text
 - Every four bits is converted to a symbol
	- – 4 bits → 24=16 symbols
 - Symbols used are 0-9, a-f
 - Often preceded with “0x” to signify that it is in hex
 - E.g. 00111100 → 0x3c

![[Screenshot_20241113_204805.png]]
![[Screenshot_20241113_204815.png]]

## ASCII Notes
- 128 “code points,” 98 of which are printable
- characters
	- – Most significant bit of each byte is unused
 - Standardized in the 60s-80s
 - Now being expanded on with Unicode
	- – UTF-8 can support over a million symbols while maintaining ASCII backwards compatibility!


## Base64 (Binary⇔Text)
 - Sometimes applications expect text documents, but a file needs to be put into that text document
	- – Example: embedding files in HTML
	- – Hex is too inefficient (4/8 bits per character used)
 - 64 code points used, each representing 6 bits
 - 0-9, a-z, A-Z, ‘+’, ‘/’
 - Sometimes padded with ‘=’ at the end to make the number of characters a multiple of four.
 - 6/8 bits of ASCII used

![[Screenshot_20241113_204924.png]]

## Ciphers
- Goal: hide data in a reversible manner
- Generally, there will be a plaintext and ciphertext
	- Plaintext is the message
	- Ciphertext is the encrypted version


![[Screenshot_20241113_205134.png]]

## Simple Substitution Cipher
- Characters in the alphabet are mapped to different characters
- Can be defeated using frequency analysis

## Vigenere Cipher
- Like a Caesar cipher, but the rotation is based on a key.
	- The key is repeated to extend it to the length of the plaintext.
- Can still be defeated using frequency analysis by figuring out the length of the key

![[Screenshot_20241113_205330.png]]

![[Screenshot_20241113_205354.png]]
![[Screenshot_20241113_205406.png]]
![[Screenshot_20241113_205418.png]]

## One-Time Pad
- If a specific key is only used once, and is at least the size of the plaintext, this is known as a “one-time pad.”
- One-time pads are completely secure, so long as the key is suitably random.
- The “pad” refers to a physical pad of paper (used by KGB spies in the early 1930s).

## Hash Function
- One way function that converts arbitrarily-sized data to a fixed size value
- Not expected to be reversible

## Uses for Hash Functions
- Hash Tables
	- Data structure with extremely efficient lookup time


## Cryptographic Hash Function
- A hash function that is...
	- One way
		- It's infeasible to find the input for a given output
	- Collision resistant
		- Two inputs are unlikely to result in the same output


## Uses for Cryptographic Hash Functions
- Password checking
- Checksums
- Alternative for storing complete copy of data when unnecessary

## Examples of Hash Functions
- Insecure
	- – MD5
	- – SHA1
- Secure
	- – SHA-2
	- – SHA-3

## Breaking Hash Functions
- Compute all possible hashes for any given input in
- advance
	- – Rainbow table
 - Common hashes are recognizable
 - Brute force based on a known pattern
	- – Hashcat
	- – John the Ripper

## Salt
- In order to avoid this problem, a random “salt” can be added to the hash function’s input and stored alongside the resulting hash
- When checking if an input matches a given hash, repeat the same process
- Advantage: hashes are unlikely to match known values because of the random data

## Recommended Challenges
- Any "easy" cryptography challenge
- (Cryptography) Vigenere
- (Cryptography) substitution (0-2)
- (General Skills) PW Crack (1-5)
- (Web Exploitation) JaWT Scratchpad