## Introduction

A Substitution Cipher is system of encryption where different symbols are substituted by a different alphabet. We can take the letter `A` and replace all occurrences with `F`, `B` with `Y`, and so on.

This gives us a key to use with encrypting and decrypting.

## Language Entropy

[xkcd (936)](https://xkcd.com/936/)

Often times, we aren't going to be given a key to the cipher. In these cases, we use a strategy from natural language processing known as language entropy. We're looking to "predict" the occurrence of a certain letter based on it's usage in the language.[1](https://ctf101.org/cryptography/what-is-a-substitution-cipher/#fn:1)

For example, knowing "vowels are used in most words" gives you a hint that reduces the computation complexity when we attempt to "guess" the usage of certain letters.

With this in mind, there are algorithms that use these clues to give you a "best estimate" what the original phrase.

If you're interested in language and information theory, there's a fascinating book on natural language processing in the footnotes!.[2](https://ctf101.org/cryptography/what-is-a-substitution-cipher/#fn:2)

https://ctf101.org/cryptography/what-is-a-substitution-cipher/