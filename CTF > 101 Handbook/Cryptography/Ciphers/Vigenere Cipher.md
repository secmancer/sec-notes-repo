## Vigenere Cipher
A Vigenere Cipher is an extended [Caesar Cipher](https://ctf101.org/cryptography/what-is-caesar-cipher-rot-13/) where a message is encrypted using various Caesar shifted alphabets. A `key` is used to determine how many shifts each letter receives. It adds an additional layer of complexity that relies on the shared key instead of a predetermined shift length.


## Cryptanalysis
The key part of breaking a Vigenere Cipher is (not a pun) the key itself. Because it repeats, it's vulnerable to brute forcing the rotation by figuring out what the length of the key is. After, frequency analysis or key elimination is used to reverse the secret. We're not going to cover it here, but check out the footnotes for more!

Online cipher solvers automatically use these steps!