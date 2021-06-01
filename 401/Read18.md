# Cryptography

One of the earliest encryption techniques is the Caesar Cipher, invented by Julius Caesar more than two thousand years ago to communicate messages to his allies.

## Encrypting a message

The Caesar Cipher is a simple substitution cipher which replaces each original letter with a different letter in the alphabet by shifting the alphabet by a certain amount.

## Decrypt message

According to historical records, Caesar always used a shift of 3. As long as his message recipient knew the shift amount, it was trivial for them to decode the message.

## Breaking a cipher

The cipher can be easily broken, especially with one of these cases: 

* The attacker knows or guessing that some sort of simple substitution cipher has been used, but not specifically that it is a Caesar scheme, the cipher can be broken using the same techniques as for a general simple substitution cipher, such as frequency analysis or pattern words. While solving, it is likely that an attacker will quickly notice the regularity in the solution and deduce that a Caesar cipher is the specific algorithm employed.

* The attacker knows that a Caesar cipher is in use, but does not know the shift value, They can use brute force attack, One way to do this is to write out a snippet of the ciphertext in a table of all possible shifts – a technique sometimes known as "completing the plain component"